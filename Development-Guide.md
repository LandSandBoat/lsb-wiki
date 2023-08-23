# Table of Contents

- [C++](#c)
- [Lua](#lua)
- [SQL](#sql)
- [Python](#python)
- [Git](Development-Guide-Git)

## Contributing

It is assumed you've read the [Contributing Guide](https://github.com/LandSandBoat/server/blob/base/CONTRIBUTING.md).

## C++

### Naming & Misc

- The STL is your friend, don't be afraid to use it.
- Be careful with `auto`, it can mask important type details.
- Be as `const` as you reasonably can.
- `UpperCamelCase` for namespaced functions and classes.
- `UPPER_SNAKE_CASE` for enums (exception for enum classes: style as classes).
- `lowerCamelCase` for everything else.

### Styling

We keep a `.clang-format` file in the root of the repo, but accept it can be difficult to set up for use on _just your changes_, as opposed to entire files that you're working with that might have legacy styling you don't want to mess with.

Here are the points from `.clang-format` explained:

#### BasedOnStyle: WebKit

When in doubt, defaulting to `WebKit style with Allman braces` is _seemingly_ a safe option.

#### AccessModifierOffset: -4

```cpp
// Correct ✔️ 
class Classname
{
public:
    Classname();

private:
    int member;
}

// Wrong ❌
class Classname
{
    public:
    Classname();

    private:
    int member;
}
```

#### AllowShortFunctionsOnASingleLine: Empty

```cpp
// Correct ✔️ 
void f()
{ 
    foo(); 
}

// Wrong ❌
void f() { foo(); }
```

#### BreakBeforeBraces: Allman

Braces should _almost always_ be on a new line.

```cpp
// Correct ✔️ 
if (x == 5)
{
    function();
}

// Wrong ❌
if (x == 5) {
    function();
}
```

#### BreakConstructorInitializers: BeforeComma & ConstructorInitializerIndentWidth: 0

```cpp
// Correct ✔️ 
Constructor(int param0, int param1)
: member0(param0)
, member1(param1)
{
}

// Wrong ❌
Constructor(int param0, int param1)
    : member0(param0), member1(param1){}
```

#### CompactNamespaces: 'false'

```cpp
// Correct ✔️ 
namespace Foo
{
    namespace Bar
    {
    }
}

// Wrong ❌
namespace Foo { namespace Bar {
}}
```

#### Cpp11BracedListStyle: 'false'

```cpp
// Correct ✔️ 
std::vector<int> x{ 1, 2, 3, 4 };

// Wrong ❌
std::vector<int> x{1, 2, 3, 4};
```

#### IndentCaseLabels: 'true'

```cpp
// Correct ✔️ 
switch(x)
{
    case 0:
    {
        break;
    }  
}

// Wrong ❌
switch(x)
{
case 0:
{
    break;
}  
}
```

- **Note**: It doesn't matter if your `break;` is inside or outside the body of your case statement - as long as it's there (if you indend it to be).

#### IndentWidth: 4

```cpp
// Correct ✔️ 
if (func())
{
    reaction();  
}

// Wrong ❌
if (func())
{
  reaction();  
}
```

#### KeepEmptyLinesAtTheStartOfBlocks: 'false'

```cpp
// Correct ✔️ 
void function(int x)
{
    doSomething(x);
}

// Wrong ❌
void function(int x)
{

    doSomething(x);
}
```

#### Language: Cpp

Yup.

#### PointerAlignment: Left

```cpp
// Correct ✔️ 
void function(CBigType* type);
void function(CBigType& type);

// Wrong ❌
void function(CBigType *type);
void function(CBigType &type);

// Wrong ❌
void function(CBigType * type);
void function(CBigType & type);
```

#### SortIncludes: 'true' & SortUsingDeclarations: 'true'

- Try to keep your `include` and `using` statements organised alphabetically, in logical blocks.

#### SpaceBeforeParens: ControlStatements

```cpp
// Correct ✔️ 
if (true)
{
    doThing();
}

// Wrong ❌
if(true)
{
    doThing();
}
```

#### Standard: Cpp11

```cpp
// Correct ✔️ 
A<A<int>>

// Wrong ❌
A<A<int> >
```

#### UseTab: Never

```cpp
// Correct ✔️
<4 spaces>

// Wrong ❌
<a tab>

// Wrong ❌
<a half-tab>
```

#### Braces Around Statements

`readability-braces-around-statements`

```cpp
// Correct ✔️ 
if (x == 5)
{
    function();
}

// Wrong ❌
if (x == 5)
    function();

// Wrong ❌
if (x == 5)
    function(21);
else
{
    function(42);
}
```

#### Breaks between consecutive conditional statements

```cpp
// Correct ✔️ 
if (thisThing())
{

}
else
{

}

if (thatThing())
{

}

// Correct ✔️ 
if (thisThing())
{

}

if (thatThing())
{

}

// Wrong ❌
if (thisThing())
{

}
else
{

}
if (thatThing())
{

}

// Wrong ❌
if (thisThing())
{

}
if (thatThing())
{

}
```

#### Breaks to split wide conditional lines - after the operator

- There is no hard rule about how wide is too wide at this time.
- Use your best judgement, but nobody likes left/right scrolling.

```cpp
// Correct ✔️
if (lotsOfStuff &&
    evenMoreStuff &&
    evenMoreStuff &&
    evenMoreStuff &&
    evenMoreStuff &&
    evenMoreStuff)
{

}

// Wrong ❌
if (lotsOfStuff
    && evenMoreStuff
    && evenMoreStuff
    && evenMoreStuff
    && evenMoreStuff
    && evenMoreStuff)
{

}

// Wrong ❌ (this is 102 chars wide)
if (lotsOfStuff && evenMoreStuff && evenMoreStuff && evenMoreStuff && evenMoreStuff && evenMoreStuff)
{

}
```

#### Casting - static_cast over C-Style

`cppcoreguidelines-pro-type-cstyle-cast`

```cpp
// Correct ✔️ 
uint32 param = static_cast<uint32>(input);

// Wrong ❌
uint32 param = (uint32)input;
```

#### Don't use static_cast to downcast: Use dynamic_cast instead

`cppcoreguidelines-pro-type-static-cast-downcast`

**NOTE**: There is a good reason for this. If you use `static_cast` and it fails, the returned pointer will **NOT NECESSARILY** be `nullptr` and any blocks checking against for `nullptr` might incorrectly succeed. `dynamic_cast` will return a `nullptr` if it fails.

```cpp
// Correct ✔️ 
if (auto PChar = dynamic_cast<CCharEntity*>(baseEntity))
{
    PChar->DoSomething()
}

// Wrong ❌
auto PChar = static_cast<CCharEntity*>(baseEntity)
PChar->DoSomething()

// Wrong ❌
if (auto PChar = static_cast<CCharEntity*>(baseEntity))
{   
    // The cast is forced, so PChar will _always_ be populated here....
    PChar->DoSomething()
}
```

#### Arg/Param spacing

```cpp
// Correct ✔️ 
auto f(0, 1, 2, 3, 4, 5, 6);

// Wrong ❌
auto f(0,1,2,3,4,5,6);
```

#### Lambdas

Formatting tools have a famously difficult time with lamdas, so we tend to wrap them in `// clang-format on/off` to ensure we can format them how we'd like.

```cpp
// Correct ✔️ 
// clang-format off
auto isEntityAlive = [&](CBigEntity* entity) -> bool
{
    return entity->isAlive;
};
// clang-format on

// Correct ✔️ 
// clang-format off
static_cast<CCharEntity>(PPlayer)->ForParty([&](CBattleEntity* entity)
{
    entity->doStuff();
});
// clang-format off

// Wrong ❌
auto isEntityAlive =
[&](CBigEntity* entity)
    {
        return entity->isAlive;
    };
```

[Back to Top](#table-of-contents)

## Lua

A lot of the styling rules from the C++ guide can and should be applied to Lua code. Here are the important points to remember when styling your Lua:

### Naming and Misc

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

### Local vars are (almost) always preferred

```lua
-- Correct ✔️ 
local var = 0

-- Wrong ❌
var = 0
```

### Allman Braces

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

### No parentheses unless needed to clarify order of operations

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

### No semicolons

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

### Formatting Conditional Blocks

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

### Placement of logical operators in long blocks

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

### No excess whitespace inside of parentheses or solely for alignment

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

### No whitespace between function name and parameters; Space between parameters

```lua
-- Correct ✔️
local function myFunction(param1, param2, param3)
end

-- Wrong ❌
local function myFunction (param1,param2,param3)
end
```

### Logical and mathematical operators should have one space padding

```lua
-- Correct ✔️
if a == b then
    a = b + c
end

-- Wrong ❌
if a==b then
    a = b+c
end
```

### Code following `end` on same indentation level should have a newline inbetween

```lua
-- Correct ✔️
if a == b then
    a = b + c
end

return a

-- Wrong ❌
if a == b then
    a = b + c
end
return a
```

### No empty newlines after function declaration, or prior to end

```lua
-- Correct ✔️
local function myFunction(param1, param2, param3)
    return param1 + param2
end

-- Wrong ❌
local function myFunction(param1, param2, param3)

    return param1 + param2
end

local function myFunction(param1, param2, param3)
    return param1 + param2

end
```

### No single-line functions or conditions

```lua
-- Correct ✔️
if a == b then
    a = b + c
end

local function myFunction(param1, param2, param3)
    return param1 + param2
end

-- Wrong ❌
if a == b then a = b + c end

local function myFunction(param1, param2, param3) return param1 + param2 end
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

[Back to Top](#table-of-contents)

## SQL

- Don't put single quotes around non string fields:

  ```sql
  42,0
  ```

  not:

  ```sql
  '42','0'
  ```

- No line breaks in the middle of a statement:

  ```sql
  INSERT INTO table_name VALUES (a,b,c,x,y,z);
  ```

  not:

  ```sql
  INSERT INTO table_name VALUES (a,b,c,
  x,y,z);
  ```

- Spaces in names get replaced with an underscore. Hyphens are allowed. Most other symbols are removed from item/mob/npc names _except_ for polutils_name or packet_name columns, where they must be escaped.
- Full lower case skill/spell/pet/ability things.
- Don't change SQL keywords to lowercase:

  ```sql
  INSERT INTO table_name
  ```

  not:

  ```sql
  insert into table_name
  ```

### Commenting in SQL

Our SQL tables are big and confusing, and they are also modified by hand. It can be very helpful to leave _short_ comments on your additions and modifications to highlight what they are.

#### Example

Without a comment, this entry is not easily human-readable:

```sql
INSERT INTO `mob_droplist` VALUES (504,0,0,1000,888,340);
```

So we instead store it as:

```sql
INSERT INTO `mob_droplist` VALUES (504,0,0,1000,888,340); -- (Colossal Calamari) seashell
```

Conversely, `Combo` weaponskill doesn't need any additional comments because it has a name field:

```sql
INSERT INTO `weapon_skills` VALUES (1,'combo',0x02020000000200000000000002000000000202000000,1,5,0,16,2000,5,1,8,0,0,0,0);
```

The format of the comment isn't massively important, but it is preferred not to use ';' as a seperator in the middle of your comment. This is a little confusing, as it's the statement-terminator in SQL.

### Placeholder Data in table rows

In general, it is preferred to comment out the entire row rather than only leaving a comment about still needing to capture it. Examples include item and NPC models. Use your best judgment and if you aren't sure you can always ask.

- If it "works" there is an unfortunate chance nobody will come back to finish it later, including the original author. Life happens, people come and go, take breaks etc.
- If its "wrong" we're likely to still get issue reports on it **because** of that partial implementation, more so than if it were completely missing.
- Experience has shown people don't often read those comments before complaining that "we" got it wrong.
- By having the partial data but commenting it out, it remains obviously incomplete and the next editor can more easily see what needs to happen.
- Example:

```sql
-- Missing model, looks like a fish. Just kidding this doesn't exist and is only a made up example
-- INSERT INTO `item_equipment` VALUES (65534,'holy_moly_mace',43,0,1048645,???,0,0,3,0,0);
```

**_And absolutely never substitute item modifiers!_**

### SQL Migrations for Schema changes

- Going forward schema changes should be accompanied by a migration script.

[Back to Top](#table-of-contents)

## Python

Python is primarily used for support scripts.

### Naming and Misc

- Python uses `lower_snake_case`

[Back to Top](#table-of-contents)
