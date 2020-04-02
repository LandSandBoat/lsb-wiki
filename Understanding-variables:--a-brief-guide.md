### Jargon:
 - Lua - This is the language in the scripts, where most people will be needing this info. And its Lua or lua, not LUA.
 - C++ or ".cpp" - This refers to those scary "core" files new people shy away from
 - var - This is shorthand for variable
 - zero out - variables that don't exist have a value of zero by design. and when we set their value to zero, they are erased automatically
 - local - That which is not global is limited to a particular section or "[scope](https://en.wikipedia.org/wiki/Scope_(computer_science))"
 - global - This means it is not limited in scope, and the variable is "visible" to the entire programs. It's everywhere.


## In lua
```lua
local stuff = thing
```
This is a local scoped lua var. These are in lua's memory space and are not saved. Only active in the scope (dis 'ere code block or file) and then forgotten.


```lua
stuff = thing
```
This is a global scoped lua var. Still in memory and not stored, but hangs out in memory forever (or till exe closes) and everything and its mom sees this. Generally a bad thing, but certain use cases exist. Like global tables full of essential things that otherwise would have been hundreds of global variables.


```lua
-- Sets a "localvar" named "string" on an entity (such as player, mob, npc) to 3
entity:setLoccalVar("string", 3)

-- Returns the var we set above so we can use or compare it
entity:getLoccalVar("string")
```
This is lost the moment the entity respawns but otherwise stays in memory. For players this means when you zone or login the localVar is gone. For monsters the distinction between "when it respawns" and "when it dies/despawns" lets you do some tricky things by setting a the var on a mob that isn't presently up or has just died and then reading it back elsewhere.


```lua
-- Stores a variable in the database table char_vars named "string" to a value of 2. 
player:setCharVar("string", 2)

-- Return the player's database var we set above so we can use or compare it
player:getCharVar("string")
```
This persists through logging out and back in and only work with player type entities. Quests and missions use a lot of these.


```lua
-- Sets a server var in the database
SetServerVar("string", 1)

-- Return value of that server var
GetServerVar("string")
```
Divides universe by zero. Don't do this. :smiley: 

(It's used for very specific circumstances where you need a global var that persists even between server restarts)

## In C++
Now, teaching you all the C++ basics is outside the scope of this document, so we'll just give a few examples while explaining some key differences in what we just saw in Lua above.
```cpp
// Set an unsigned 8 bit integer variable named exampleOne to the value of zero
uint8 exampleOne = 0;

// Set a floating point variable named exampelTwo to the value of 3.50
float exampleTwo = 3.50f;

// Set a string variable to the specified text
std::string exampleThree = "that'll be tree fiddy";

// Here the compiler tries to figure out what you wanted instead of you declaring the type.
auto ExampleWhateverMan = 666;
```
As you can see, unlike Lua you need to say what kind of data you wanted your variable to hold (or "auto" all the things and risk your compiler giving you surprise optimization you didn't know you wanted).

```cpp
m_PBaseEntity->SetLocalVar(varName, value);
```
This is equivalent to `entity:setLocalVar(varName, value)` in Lua.

As for charVar and ServerVar are both done entirely by SQL queries in their bindings, and have never had to be done in core code thus far.
