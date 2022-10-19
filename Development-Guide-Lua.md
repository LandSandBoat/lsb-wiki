# Development Guide (Lua)

A lot of the styling rules from the C++ guide can and should be applied to Lua code. Here are the important points to remember when styling your Lua:

## Naming and Misc

- Our lua functions and members are typically `lowerCamelCased`, with few exceptions.
- Make sure you check out `scripts/globals/npc_util.lua` for useful tools and helpers.
- If you're going to cache a long table entry into a var with a shorter name, make sure that name still conveys the original meaning.

```lua
-- Correct ✔️
local copCurrentMission = player:getCurrentMission(xi.mission.log_id.COP)
local copMissionStatus = player:getCharVar("PromathiaStatus")
local sandyQuests = xi.quest.id.sandoria

-- Wrong ❌
local currentMission = player:getCurrentMission(xi.mission.log_id.COP)
local missionStatus = player:getCharVar("PromathiaStatus")
local quests = xi.quest.id.sandoria
```

#### Local vars are (almost) always preferred

```lua
-- Correct ✔️ 
local var = 0

-- Wrong ❌
var = 0
```

#### Allman Braces

```lua
-- Correct ✔️ 
local table =
{
    content = 1,
}

-- Wrong ❌
local table = {
    content = 1,
}
```

**NOTE:** The final entry in a multi-line table should have a comma after it.

#### No parentheses unless needed to clarify order of operations

```lua
-- Correct ✔️ 
if condition1 == 1 then
    trigger()
end

-- Correct ✔️ 
if condition1 and (condition2 or condition3) then
    trigger()
end

-- Wrong ❌
if (condition1 == 1) then
    trigger()
end
```

#### No semicolons

```lua
-- Correct ✔️ 
local x = 42
trigger(42)

-- Wrong ❌
local x = 42;
trigger(42);

-- Wrong ❌
local x = 42; trigger(42);
```

#### Formatting Conditional Blocks

```lua
-- Short - Correct ✔️
if condition then
    bla()
end

-- Long or many multiple conditions - Correct ✔️
if
    condition1 and
    condition2 or
    not condition3
then
    bla()
end

-- Wrong ❌
if  condition1 then
    bla()
end

-- Wrong ❌
if condition1 and condition2 and
    not condition3 then
    bla()
end

-- Wrong ❌
if condition1 and condition2 and
    not condition3
then
    bla()
end
```

#### Placement of logical operators in long blocks

- `not` before, `and/or` after

```lua
-- Correct ✔️
if
    condition1 and
    condition2 or
    not condition3
then
    bla()
end

-- Wrong ❌
if
    condition1
    and condition2
    or not condition3
then
    bla()
end
```

#### No excess whitespace inside of parentheses or solely for alignment

```lua
-- Correct ✔️ 
if condition1 and (condition2 or condition3) then
    trigger()
end

-- Wrong ❌
if condition1 and ( condition2 or condition3 ) then
    trigger()
end

-- Wrong ❌
if
      condition1 and 
    ( condition2 or condition3 )
then
    trigger()
end
```

#### Inline tables

##### THIS IS THE ONE EXCEPTION TO THE GLOBAL NEWLINE-BRACE RULES

```lua
-- Correct ✔️ 
xi.func({
  entry = 1,
  entry = 2,
})

-- Wrong ❌
xi.func(
    {
        entry = 1,
        entry = 2,
    }
)
```
