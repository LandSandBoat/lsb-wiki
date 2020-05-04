# 1. Common issues

## Gil not sent to the Delivery Box from the Auction House

One possible fix: Execute HeidiSQL > select your session and connect to it > select "tpzdb" > File > Run SQL file... > select the triggers.sql file from the \topaz\sql folder > Open.

# 2. Tweaks

## Make your character a Game Master

Execute HeidiSQL > connect to your database > select "chars" > "Data" tab > "gmlevel" column > modify the value from 0 to 5 (maximum level) > close HeidiSQL.

Change zone in game to apply.

Type "!command" in game (refer to the \topaz\scripts\commands folder for a list of commands).

!togglegm: no more aggro.

!togglegm + /anon: invisible through /search.

!hide: invisible to players.

## Unlock Superior levels (to wear particular items)

\topaz\src\map\packets\char_stats.cpp:

Replace:
```
//0x52 = superior level (1 or 2)
```

by:
```
ref<uint8>(0x52) = X; (< expected level/5)
```

or:
```
ref<uint8>(0x52) = PChar->GetMLevel () == 99? 5: 0;
```
Rebuild the solution.