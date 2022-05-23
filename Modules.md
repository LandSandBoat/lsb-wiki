# Modules

Please see `modules/init.txt` for how to load modules.

## Lua Modules

```lua

```

## CPP Modules

Place a `.cpp` file somewhere in the `modules/` subfolder and enable it with `init.txt`. You'll then need to re-configure
your build using CMake. Towards the end of configuration, it will log which module files have been added to the build:

```txt
-- Adding module files to build: C:/ffxi/server/modules/era/cpp/test.cpp
```

You can then continue your build as normal, and your module files will be compiled at the end.

```cpp
#include "map/utils/moduleutils.h"

// CPP Modules are calls synchronously, so you have safe access to the main sql connection, the Lua state,
// logging, and anything else you might regularly use.
#include "common/logging.h"
#include "common/sql.h"
#include "lua/luautils.h"
#include "utils/itemutils.h"

namespace
{
    constexpr uint16 HOURGLASS_ID = 4237;

    uint32 currentEpoch()
    {
        return static_cast<uint32>(time(nullptr));
    }
};

//       |-- Name your module something unique.
//       v                    v-- You must inherit from CPPModule.
class TestModule : public CPPModule
{
    // In Lua, the ':' function calling syntax is just syntactic sugar for:
    //     function(object, param0, param1, ...)
    // This is what will be required if you want to inject your own bindings.
    //                         v----object----v           v-param0-v    v-param1-v
    void createHourglass(CLuaBaseEntity* PLuaBaseEntity, uint8 zoneID, uint32 token)
    {
        TracyZoneScoped;

        CBaseEntity* PEntity = PLuaBaseEntity->GetBaseEntity();
        if (PEntity->objtype != TYPE_PC)
        {
            return;
        }

        auto ret = sql->Query("SELECT value FROM server_variables WHERE name = '[DYNA]Token' LIMIT 1;");
        if (ret != SQL_ERROR && sql->NumRows() && sql->NextRow())
        {
            auto res = sql->GetUIntData(0);
            if (res == HOURGLASS_ID)
            {
                CItem* PItem = itemutils::GetItem(HOURGLASS_ID);
                PItem->setQuantity(1);

                ref<uint8>(PItem->m_extra,  0x02) = 1;
                ref<uint32>(PItem->m_extra, 0x04) = PEntity->id;
                ref<uint32>(PItem->m_extra, 0x0C) = currentEpoch();
                ref<uint8>(PItem->m_extra,  0x10) = zoneID;
                ref<uint32>(PItem->m_extra, 0x14) = token;
            }
        }
    }

    //     v-- OnInit is required for all CPP modules.
    void OnInit() override // Called just before the server is ready to run.
    {
        // player:createHourglass(zoneID, token)
        lua["CBaseEntity"]["createHourglass"] = &TestModule::createHourglass;

        // You could also use lambdas, if you wish
        // mob:anotherFunction()
        lua["CBaseEntity"]["anotherFunction"] = [](CLuaBaseEntity* PLuaBaseEntity) -> void
        {
            TracyZoneScoped;

            CBaseEntity* PEntity = PLuaBaseEntity->GetBaseEntity();
            if (PEntity->objtype != TYPE_PC)
            {
                return;
            }

            // ...
        };
    }

    // The following are optional:
    // void OnZoneTick(CZone* PZone){};          // Called at the end of Zone_Server's tick.
    // void OnTimeServerTick(){};                // Called at the end of time_server's tick.
    // void OnCharZoneIn(CCharEntity* PChar){};  // Called just before a character finished zoning in.
    // void OnCharZoneOut(CCharEntity* PChar){}; // Called just before a character starts zoning out.
};

// You must call this to register your module with the program!
REGISTER_CPP_MODULE(TestModule);
```

## SQL Modules

SQL modules are just additional SQL files that are run at the end of `dbtool.py` updates, after all the other SQL files.
They still need to be enabled with `init.txt`.

```sql
-- Setting all 2HR abilities to 2HR cooldown
UPDATE abilities SET recastTime = "7200" WHERE name = "mighty_strikes";
UPDATE abilities SET recastTime = "7200" WHERE name = "hundred_fists";
-- ...
```
