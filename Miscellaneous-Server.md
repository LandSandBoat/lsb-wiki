## Common Tasks
### Generating LandSandBoat patch notes
You can use `server\tools\generate_changelog.py` to generate patch notes from LandSandBoat to publish as-is, or to supplement your own patch notes.
By default, `server\tools\generate_changelog.py` will generate patch notes for the last 14 days, but it accepts an argument if you wanted to use an arbitrary number of days: <code>tools\generate_changelog.py 30</code> will generate 30 days. We automatically generate patch notes on the 1st and 15th day of the month, and store them here: https://github.com/LandSandBoat/server/tree/website/changelogs.

## Common Issues
### Gil not sent to the Delivery Box from the Auction House
One possible fix: Execute HeidiSQL > select your session and connect to it > select "xidb" > File > Run SQL file... > select the triggers.sql file from the `server\sql` folder > Open.

### Version Mismatch
**WE STRONGLY ADVISE AGAINST LOCKING THE SERVER TO OLDER VERSIONS. IT IS A UNIVERSALLY BAD IDEA.** It *will* cause issues even *if* you manage to keep both server and client versions on par!

If the server (LandSandBoat) and the client (Final Fantasy XI) don't share the same version, you'll probably get this error in the xi_connect.exe log window:
```
[Error] lobbyview_parse: Incorrect client version: got 000000xx_x, expected 000000xx_x
[Error] lobbyview_parse: The server must be updated to support this client version
```
**Copy** the following file from the `server\settings\default\` folder into the `server\settings\` folder and open the copied file (with the default Windows text editor (Notepad) or an external one (like  [Notepad++](https://notepad-plus-plus.org/)):

* login.lua

then modify this line:

> VER_LOCK = 2,

(replace **2** with **0**)

then save the changes and restart the **xi_connect.exe** server.


## Tweaks
### Setting up an automated Auction House with Python
#### Installing
Python and the MySQL Python Connector are needed and should already be installed if you previously followed our [Server-Setup-and-Maintenance-[Windows-10] Windows 10 installation setup guide].

Right click wherever you want to download the repository > Git Clone... > URL: https://github.com/AdamGagorik/pydarkstar.git > OK > then Close when it's done.

Its setup instructions (found **[HERE](http://adamgagorik.github.io/pydarkstar/generated/setup.html)**) are focused on a package manager named Anaconda. The below instructions are focused on pip, which comes with the stock python installer. Anaconda may work better for you if the command line is scary.

***Whichever you choose, it is important to note that LSB doesn't maintain or provide support for pydarkstar - its a nice thing that happens to work. PLEASE contact its author NOT US, for any that wasn't a direct result of us screwing up our guide! Thanks for your understanding.***

#### To get started via pip: 

Right click + holding the Shift key > context menu: Open command window here/Open PowerShell window here, then type:
```
py -3 -m pip
```
then enter each of these commands (hit "Enter" after each one) and it will download and install automatically:
```
py -3 -m pip install beautifulsoup4
py -3 -m pip install pymysql
py -3 -m pip install sqlalchemy
```
Double click on `\pydarkstar\makebin.py` to create base files then open `\pydarkstar\bin\config.yaml` with a text editor (default options are listed below, you can edit them at your convenience):
```
name: Zissou (will be the name of the bot displayed in the AH lists, buying and selling items)
database: xidb (change it accordingly to your database's name)
password: root (replace with your MariaDB password)
restock: 3600 (seconds between each automatic restock)
tick: 30 (seconds between each purchase will be made by the bot)
stock01: 5 (number of single items that will be restocked each tick)
stock12: 5 (number of stacks items that will be restocked each tick)
```

#### Running
1. ~~Execute \pydarkstar\pydarkstar\bin\scrub.py to build up the items list from https://www.ffxiah.com/ (will take some time). Unfortunately you can't select the server from which the prices are pulled, if I'm correct Bahamut is the server by default. Rerun it if you want to update prices automatically.~~ **Do not run the scrape to get new prices from ffxiah. Just don't. The stock file was heavily edited to ensure you didn't create a gil printing press on your server.**

2. Execute `\pydarkstar\pydarkstar\bin\broker.py`: Script that will automatically buy/sell stuff. Let it run in the background.

3. Executing `\pydarkstar\pydarkstar\bin\refill.py` will restock items automatically.

4. Editing prices manually: open `\pydarkstar\bin\items.csv` with a text editor (0 = non listed item, add them by referring to the IDs in `\server\sql\item_equipment.sql` if necessary) and change prices accordingly.

### HeidiSQL useful querys:

```
UPDATE auction_house SET seller_name = 'Your-choice-here';
UPDATE auction_house SET buyer_name = 'Your-choice-here';
UPDATE auction_house SET buyer_name = 'Your-choice-here' where buyer_name is null or buyer_name = 'Your-choice-here';
UPDATE auction_house SET sell_date = 'Your-choice-here' where sell_date = 'Your-choice-here';
```

### Updating Python
Updating Python: Default location of the Python installation files is: `C:\Users\Username\AppData\Local\Programs\Python`, when updating you may want to relocate old files from your old version's folder to the new one (copy/paste).

Updating modules: Make sure you check if your modules are up to date from time to time (you'll probably get reminded while running migrations scripts). To do so, open a command prompt like stated above and enter:

`py -3 -m pip install --upgrade Modulename
`

### Useful GM Commands
Type `!command` in game (for other GM commands to use in place of **!command**, refer to: `\server\scripts\commands`). 

!togglegm: no more aggro and the GM icon next to the character name

!togglegm + /anon: invisible through /search.

!hide: switches between being visible/invisible to players.

### Unlock Superior (Su) levels (to wear particular items)
In ``\server\src\map\packets\char_stats.cpp``:

Replace:
```cpp
ref<uint8>(0x52) = PChar->getMod(Mod::SUPERIOR_LEVEL);
```
with:
```cpp
ref<uint8>(0x52) = X; // replace X with desired superior level
```
or:
```cpp
ref<uint8>(0x52) = PChar->GetMLevel() == 99 ? 5 : 0; // level 99 auto superior 5
```
Rebuild the solution.


### Change your MariaDB password
Open: Start Menu > "MariaDB xx.x (x64)" folder > "MySQL Client (MariaDB xx.x)".

In the prompt command, you will be prompted to enter your current MySQL DB password.  Do so, hit "Enter", then enter the following commands:
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

How to check if it was changed correctly (while still having the same prompt command open):
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

### How do I set JP Midnight?
JP midnight is now coded to align with the retail JST midnight regardless of your local timezone setting and manual configuration is no longer required. There is no setting for JP Midnight and we do not recommend altering server timing behaviour as the client has hard-coded expectations that certain events and resets will occur at certain times.

### Auto-Starting the Server
#### Linux
Linux users can create several systemd services to automate the servers (make sure to update `/path/to/topaz`, and the User/Group):

```
#topaz.service

[Unit]
Description=Topaz - FFXI Server Emulator
After=mysql.service

[Service]
Type=oneshot
ExecStart=/bin/true
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

```
#topaz_game.service

[Unit]
Description=Topaz Game Server
Wants=network.target
StartLimitIntervalSec=120
StartLimitBurst=5
PartOf=topaz.service
After=topaz.service

[Service]
Type=simple
Restart=always
RestartSec=5
User=topaz
Group=topaz
WorkingDirectory=/path/to/topaz
# For multiple map servers:
# - Make a copy of this file for each server. Rename appropriately, e.g. topaz_game-cities.service
# - Add this to a file named ip.txt in the topaz folder, replacing YOUR_PUBLIC_IP with your IP: "IP=YOUR_PUBLIC_IP"
# - Change the zone ports in zone_settings table. A custom.sql file is useful for this.
# - Remove the line below, 'ExecStart=/path/to/topaz_game'.
# - Uncomment and edit the 2 lines below with the appropriate port and log location for each zone server.
#EnvironmentFile=/path/to/topaz/ip.txt
#ExecStart=/path/to/topaz/topaz_game --ip $IP --port 54230 --log /path/to/log/map_server.log
ExecStart=/path/to/topaz/topaz_game

[Install]
WantedBy=topaz.service
```

```
#topaz_connect.service

[Unit]
Description=Topaz Connect Server
Wants=network.target
StartLimitIntervalSec=120
StartLimitBurst=5
PartOf=topaz.service
After=topaz.service

[Service]
Type=simple
Restart=always
RestartSec=5
User=topaz
Group=topaz
WorkingDirectory=/path/to/topaz
ExecStart=/path/to/topaz/topaz_connect

[Install]
WantedBy=topaz.service
```

```
#topaz_search.service

[Unit]
Description=Topaz Search Server
Wants=network.target
StartLimitIntervalSec=120
StartLimitBurst=5
PartOf=topaz.service
After=topaz.service

[Service]
Type=simple
Restart=always
RestartSec=5
User=topaz
Group=topaz
WorkingDirectory=/path/to/topaz
ExecStart=/path/to/topaz/topaz_search

[Install]
WantedBy=topaz.service
```
After adding these to `/etc/systemd/system/`, run `systemctl daemon-reload` followed by `systemctl enable topaz_game topaz_connect topaz_search`. You can start/stop all the servers at once with `systemctl start/stop topaz` or each individual service separately. To enable auto-start, type `systemctl enable topaz`. Make sure topaz is in a location accessible to the user that will be running the service, and the correct permissions are set.

### Automatically give new players a server linkshell
In `server\scripts\globals\player.lua` find the following line:
```lua
player:setNewPlayer(true) -- apply new player flag
```
and add the following line:
```lua
player:addLinkpearl("YOURLS", true)
```
(replace **YOURLS** with the desired linkshell name)
(leave the quotation marks surrounding the desired linkshell name)

The second parameter **true** will equip the linkpearl in slot 2. Change to **false** if you want to just place it in the inventory without equipping. ***NOTE THAT THE LINKSHELL MUST ALREADY EXIST FIRST.***

### Announce to entire server when a player logs in
At the end of `LoadChar(...)` in `\server\src\map\utils\charutils.cpp` you can add the following snippet to announce when a player logs in for the first time in their play session:
```cpp
        if (zoning == 2)
        {
            // Send message to all logged in players
            zoneutils::ForEachZone([&](CZone* PZone) {
                PZone->ForEachChar([&](CCharEntity* PLoggedInChar) {
                    PLoggedInChar->pushPacket(new CChatMessagePacket(PLoggedInChar, CHAT_MESSAGE_TYPE::MESSAGE_SYSTEM_1,
                        fmt::format("{} has logged into the server.", PChar->GetName())));
                });
            });
        }
```
