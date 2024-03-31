**TLDR:**

>- Retire the Windows 32-bit build.
>- Updated the existing `mariadb-connector-c` library.
>- Introduce the `mariadb-connector-cpp` library, which wraps the `mariadb-connector-cpp` with better usage patterns.
>- Add an API on top of `mariadb-connector-cpp` that can be used alongside our current SQL usage.
>- All instances of `sql` global object are replaced with `_sql` because of clashing symbols in the new library. The goal is to eventually replace these with their new `db` namespace equivalents.
>- The new API provides:
>    - Thread-safe usage.
>    - Protection from clobbering your results by interleaving queries.
>    - Option to extract column results of queries by column name rather than by index.
>    - Additional safety through use of prepared statements.
>    - Equivalent-or-better performance.

## Introduction

## The PR

<https://github.com/LandSandBoat/server/pull/4601>

## Background

## Goals

### Safety

Prepared statements

### Developer Quality of Life

## What does this mean for my server?

## What's Next?

## Usage and Query Migration Guide

The new API looks like this:

- note that `ret` (Return Code) and `rset` (Result Set) are very different things!

### `db::query`

```cpp
// Send in a simple string query and don't check the results
auto query = fmt::format("UPDATE char_stats SET zoning = 0 WHERE charid = {}", PChar->id);
db::query(query);

// Send in a simple string query and check the results
if (!db::query(...))
{
    ShowError("Failed to update daily tally points");
}
else
{
    ShowDebug("Distributed daily tally points");
}

// Send in a simple string query and extract out a single result
auto rset = db::query(...);
if (rset && rset->rowsCount() && rset->next() // If there is a result. Equivalent to `if (ret != SQL_ERROR && _sql->NumRows() != 0 && _sql->NextRow() == SQL_SUCCESS)`
{
    const auto itemid = rset->getInt("itemid"); // Extract data by column name from the `rset`, not the database connection object
    ...
}

// Send in a simple string query and extract out multiple rows of results
auto rset = db::query(...);
if (rset && rset->rowsCount()) // If there are results: Equivalent to `if (ret != SQL_ERROR && _sql->NumRows() != 0)`
{
    while (rset->next()) // Iterate over your results. Equivalent to `while (_sql->NextRow() == SQL_SUCCESS)`
    {
        const auto itemid = rset->getInt("itemid"); // Extract data by column name from the `rset`, not the database connection object
        ...
    }
}
```

### `db::preparedStmt`

There is a lot of plumbing going on behind the scenes to shield you from having to manage your own prepared statement objects.
They are lazily constructed and cached on your behalf.

```cpp
const char* query = "SELECT set_blue_spells FROM "
                    "chars WHERE charid = (?);";  // <-- Note the dynamic parameter slot here

// The prepared statement will be created, cached, and bound for you behind the scenes
auto rset = db::preparedStmt(query, PChar->id);
if (rset && rset->rowsCount() && rset->next()) // Inspect and iterate as normal
{
    db::extractFromBlob(rset, "set_blue_spells", PChar->m_SetBlueSpells);
}
```
