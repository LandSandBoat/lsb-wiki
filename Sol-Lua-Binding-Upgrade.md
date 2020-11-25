### Intro
If you're here, you're probably aware of how we use Lua (Portuguese for Moon, not an acronym) as a scripting language for quick iteration, and to lower the barrier to entry for newcomers. Aside from a couple of quirks that get under peoples' skin (1-indexed arrays); it is a wonderful language that is very fast to pick up and has surprising versatility.

In order to use Lua alongside our Core C++ code, we need to `bind` C++ functions to Lua, and represent `C++ Types` as `Lua Usertypes`. This is achieved by using a `binding system`, or `binding library`. 

Our current binding system is called [Lunar](http://lua-users.org/wiki/CppBindingWithLunar) and was originally published as a code snippet around 2009. At the time, there probably wasn't much available in terms of binding libraries, so this would have been a godsend in terms of "easy" interop with C++. Unfortunately, Lunar hasn't been upgraded or iterated on... ever. We haven't touched it (apart from formatting passes) since [Sep 16, 2011](https://github.com/project-topaz/topaz/commit/7a160120a7b7313cbfc1b5483627cebc24776ada#diff-605911436f6554e7f7420de334e67cd1d76100e8c8f33559c4d9733db3011b70).

If it was rock-solid and easy to use/understand/extend, then we would be perfectly fine to leave it alone forever. This however is not the case. The binding system and the process of getting information into and out of the Lua state is fragile and arcane. Much developer time has been wasted "fiddling with the stack". Since our adoption of Lunar pre-2011, the Lua-binding ecosystem has moved on and there are a wealth of viable libraries allowing for safer usage, modern workflows, and easier to understand/maintain code.

The most promising and well supported library at the moment is **[sol](https://github.com/ThePhD/sol2)** (sol2 v3, referred to as Sol/sol for clarity).

### Examples
#### Basic
```cpp
int main()
{
    sol::state lua(); // Create lua state
    lua.open_libraries(); // Open all lua standard libs
  
    lua.script("print('Hello from Lua!')");

    return 0;
}
```

#### Lua from C++
```cpp
int main()
{
    sol::state lua(); // Create lua state
    lua.open_libraries(); // Open all lua standard libs
  
    lua.script("function callMe(str) print(str) end");

    lua["callMe"]("Test String");

    return 0;
}
```

#### C++ from Lua
```cpp
int main()
{
    sol::state lua(); // Create lua state
    lua.open_libraries(); // Open all lua standard libs
  
    auto nativeFunc = [](std::string str) { std::cout << str << "\n"; };
    
    lua["nativeFunc"] = nativeFunc;

    lua.script("nativeFunc('Hello from nativeFunc!')");

    return 0;
}
```

#### Bind free functions
```cpp
namespace luautils
{
    void sayHello()
    {
        std::cout << "Hello!\n";
    }
}

int main()
{
    sol::state lua(); // Create lua state
    lua.open_libraries(); // Open all lua standard libs
  
    lua.set_function("sayHello", &luautils::sayHello);

    lua.script("sayHello()");

    return 0;
}
```

#### Simple Usertypes
```cpp
struct Entity
{
    int ID;
    int getID()
    {
        return ID;
    }
};

int main()
{
    sol::state lua(); // Create lua state
    lua.open_libraries(); // Open all lua standard libs
  
    lua.new_usertype<Entity>("Entity",
        "getID()", &Entity::getID()
    );
    
    lua.script("function printEntityID(entity) print(entity:getID()) end");

    auto entity = Entity{42};

    lua["printEntityID"](entity);

    return 0;
}
```

#### Binding Wrappers for Usertypes
```cpp
// Underlying Entity
struct Entity
{
    int ID;
    int Zone;

    int getID()
    {
        return ID;
    }

    int getZone()
    {
        return Zone;
    }
};

// "Wrapper" around underlying Entity
struct LuaEntity
{
    Entity* m_PEntity;

    int getID()
    {
        return m_PEntity->ID;
    }

    int getZone()
    {
        return m_PEntity->Zone;
    }

    int getLongID()
    {
        // Other logic can live here <--
        return otherutils::makeLongID(m_PEntity->ID, m_PEntity->Zone);
    }
};

int main()
{
    sol::state lua(); // Create lua state
    lua.open_libraries(); // Open all lua standard libs
  
    lua.new_usertype<LuaEntity>("LuaEntity",
        "getID()", &LuaEntity::getID(),
        "getZone()", &LuaEntity::getZone(),
        "getLongID()", &LuaEntity::getLongID()
    );

    lua.script("function printEntityInfo(entity) print(entity:getID()); print(entity:getZone()); print(entity:getLongID()); end");

    auto entity = Entity{42, 99};
    auto luaEntity = LuaEntity{entity}

    lua["printEntityInfo"](luaEntity);

    return 0;
}
```

#### Basic interop with Lunar
```cpp
uint32 someExistingBinding(lua_State* L)
{
    sol::state_view lua(L); // Create non-owning view into existing lua state
  
    ... // Continue using 'lua' and the sol functionality...

    return 0;
}
```