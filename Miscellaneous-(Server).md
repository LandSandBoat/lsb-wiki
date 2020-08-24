# 1. Common issues

## Gil not sent to the Delivery Box from the Auction House

One possible fix: Execute HeidiSQL > select your session and connect to it > select "tpzdb" > File > Run SQL file... > select the triggers.sql file from the \topaz\sql folder > Open.

# 2. Tweaks

## Setting up an automated Auction House with Python.

Python and the MySQL Python Connector are needed and should be already installed if you previously followed our [Windows 10 installation setup guide](https://github.com/project-topaz/topaz/wiki/Server-Setup-and-Maintenance-[Windows-10]).

Right click wherever you want to download the repository > Git Clone... > URL: https://github.com/AdamGagorik/pydarkstar.git > OK > then Close when it's done.

/!\ Running topaz-search.exe in the background (as administrator) is mandatory /!\

Right click + holding the Shift key > context menu: Open command window here/Open PowerShell window here.: then type (**use "pip3" (default) or "pip" in each command, the one that works for you**):

```
py -m pip3
```

then enter each of these commands (hit "Enter" after each one) and it will download and install automatically:

```
py -m pip3 install beautifulsoup4
py -m pip3 install pymysql
py -m pip3 install sqlalchemy
```

Double click on \pydarkstar\makebin.py to create base files then open \pydarkstar\bin\config.yaml with a text editor (default options are listed below, you can edit them at your convenience):

```
name: Zissou (will be the name of the bot displayed in the AH lists, buying and selling items)
database: dspdb (change it accordingly to your database's name)
password: root (replace with your MariaDB password)
restock: 3600 (seconds between each automatic restock)
tick: 30 (seconds between each purchase will be made by the bot)
stock01: 5 (number of single items that will be restocked each tick)
stock12: 5 (number of stacks items that will be restocked each tick)
```

1. Execute \pydarkstar\pydarkstar\bin\scrub.py to build up the items list from https://www.ffxiah.com/ (will take some time). Unfortunately you can't select the server from which the prices are pulled, if I'm correct Bahamut is the server by default. Rerun it if you want to update prices automatically.

2. Execute \pydarkstar\pydarkstar\bin\broker.py: Script that will automatically buy/sell stuff. Let it run in the background.

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

Updating Python: Default location of the Python installation files is: C:\Users\Username\AppData\Local\Programs\Python, when updating you may want to relocate old files from your old version's folder to the new one (copy/paste).

Updating modules: Make sure you check if your modules are up to date from time to time (you'll probably get reminded while running migrations scripts). To do so, open a command prompt like stated above and enter:
```
py -m pip3 install --upgrade Modulename
```

---

## Make your character a Game Master

Open up your SQL editor > connect to your database > select "chars" > "Data" tab > "gmlevel" column > modify the value from 0 to 5 (maximum level) > close your editor.

Change zone in game to apply.

Type "!command" in game (for said "command" refer to the ones listed here: https://github.com/project-topaz/topaz/tree/release/scripts/commands).

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
