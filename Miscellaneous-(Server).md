# 1. Common issues

## Gil not sent to the Delivery Box from the Auction House

One possible fix: Execute HeidiSQL > select your session and connect to it > select "tpzdb" > File > Run SQL file... > select the triggers.sql file from the \topaz\sql folder > Open.

# 2. Tweaks

## Setting up an automated Auction House with Python.

* Download and install [Python (latest version)](https://www.python.org/downloads/): Accept defaults.

Right click wherever you want to download the repository > Git Clone... > URL: https://github.com/AdamGagorik/pydarkstar.git > OK > then Close when it's done.

/!\ Running topaz-search.exe in the background (as administrator) is mandatory /!\

Right click + holding the Shift key > context menu: Open command window here/Open PowerShell window here.: then type:

```
py -m pip3
```

Enter > then enter each of these commands (followed by "Enter" each time) and le it download stuff:

```
py -m pip3 install beautifulsoup4
py -m pip3 install pymysql
py -m pip3 install pyyaml
py -m pip3 install pip
py -m pip3 install sqlalchemy
```

Double click on \pydarkstar\makebin.py to create base files then open \pydarkstar\bin\config.yaml with a text editor (default options listed):

```
name: Zissou (name of the bot displayed in game)
database: dspdb (change it accordingly to your database's name)
password: root (replace with your MariaDB password)
restock: 3600 (seconds between each automatic restock)
tick: 30 (seconds between the bot buying stuff listed on the Auction House)
stock01: 5 (number of single items that will be restocked each tick)
stock12: 5 (number of stacks items that will be restocked each tick)
```

1. Execute \pydarkstar\pydarkstar\bin\scrub.py to build up the items list from https://www.ffxiah.com/ (will take some time). Unfortunately you can't select the server from which the prices are pulled, if I'm correct Bahamut is by default. Rerun it if you want to update prices automatically.

2. Execute \pydarkstar\pydarkstar\bin\broker.py = Script that will automatically buy/sell stuff. Let it run in the background.

---

Executing \pydarkstar\pydarkstar\bin\refill.py will restock items automatically.

Editing prices manually: open \pydarkstar\bin\items.csv with a text editor (0 = non listed item, add them by referring to the IDs in \topaz\sql\item_equipment.sql if necessary) and change prices accordingly.

HeidiSQL useful querys:

```
UPDATE auction_house SET seller_name = 'Your-choice-here';
UPDATE auction_house SET buyer_name = 'Your-choice-here';
UPDATE auction_house SET buyer_name = 'Your-choice-here' where buyer_name is null or buyer_name = 'Your-choice-here';
UPDATE auction_house SET sell_date = 'Your-choice-here' where sell_date = 'Your-choice-here';
```

---

/!\

The search_server.exe will list errors ("[SQL] DB error - Duplicate entry [...]"), edit every occurrence you'll find of "2020" in the pydarkstar\auction\manager.py file (L131, 139, 150, 158) to "2099". Save. 

---

## Make your character a Game Master

Open up your SQL editor > connect to your database > select "chars" > "Data" tab > "gmlevel" column > modify the value from 0 to 5 (maximum level) > close your editor.

Change zone in game to apply.

Type "!command" in game (refer to the \topaz\scripts\commands folder for a list of commands).

!togglegm: no more aggro.

!togglegm + /anon: invisible through /search.

!hide: invisible to players.

---

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

---

## Change your MariaDB password

Open: Start Menu > "MariaDB xx.x (x64)" folder > "MySQL Client (MariaDB xx.x)".

Then in the prompt command, enter the following commands:

```
Enter password: Your-current-MariaDB-password
```
Hit "Enter", then type:

```
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('Your-new-desired-password');
```
Hit "Enter" (returned message: "Query OK, 0 rows affected"), then type:

```
FLUSH PRIVILEGES;
```
Hit "Enter" (returned message: "Query OK, 0 rows affected"), then type:

```
exit
```
Hit "Enter" (returned message: "Bye").

---

## How to check if it was changed correctly (while still having the same prompt command open)

```
mysql -u root -p
```
Hit "Enter", then type:
```
Enter password: Your-new-MariaDB-password
```
Hit "Enter".
```
exit
```
Hit "Enter" (returned message: "Bye").

Done.

---

## Change default settings (covers XP, speed, fame rate, skill rate, merit points held, HP/MP of mobs, etc.)

Open up these files in your preferred text editor and change values accordingly: 

\topaz\conf\map.conf (after getting it out of the default folder). Save, then reboot your servers.

\topaz\scripts\globals\settings.lua. Save, use the GM command !reloadglobal settings in game or reboot your servers.
