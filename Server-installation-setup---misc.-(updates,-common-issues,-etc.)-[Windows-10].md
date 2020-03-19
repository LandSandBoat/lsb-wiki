## 1. Software needed:

* Download and install [Visual Studio Community 2019](https://visualstudio.microsoft.com/vs/community/): Under "Workloads" > check "Desktop development with C++".
* Download and install [Git for Windows](https://gitforwindows.org/): Nothing to do in particular during the installation.
* Download and install [TortoiseGit](https://tortoisegit.org/): Nothing to do in particular during the installation.
* Download and install [MariaDB](https://mariadb.org/): You can install HeidiSQL from there or get it separately, just remember the password you set for MariaDB during the installation.
* Download and install [HeidiSQL](https://www.heidisql.com/): Nothing to do in particular during the installation.
* Download and install [Python 3.7+](https://www.python.org/downloads/): Accept defaults

## 2. Download the source code:

1. Right click wherever you want to download the repository > Git Clone... > URL: https://github.com/project-topaz/topaz.git > OK > then Close when it's done. 

2. Don't forget about Navmeshes (https://github.com/project-topaz/xiNavmeshes.git): right click on the freshly downloaded "topaz" folder > TortoiseGit > Submodule Update... > OK > then Close when it's done.

## 3. Prepare the database:

1. Execute HeidiSQL and click on "New" (bottom left) then name your session as you wish > Password: Password previously saved from the MariaDB installation > Open > right click on it (left) > Create new > Database > name it "tpzdb" > OK.

2. Select "tpzdb" > File > Run SQL file... > select every .sql file from the \topaz\sql folder > Open > click on "Refresh" (F5) once everything is done. Alternatively, you can run the Database_initial_setup.bat file located in the \topaz\tools folder. 

* Don't forget to verify that the IP address displayed in the "zoneip" column ("Data" tab) of the zone_settings table is the correct one (local (127.0.0.1) by default). In case you need to update all the lines at once: Click on the "Query" tab then type:

> UPDATE zone_settings SET zoneip = '**your.IP**';

Click on "Execute SQL..." (blue icon on top) > Yes.

## 4. Build the servers:

1. Execute Visual Studio Community 2019: Open a project or solution (on the right) > select the "topaz.sln" file from the \topaz\win32 folder > Open.

2. Once it's loaded > Build > Build Solution.

3. To confirm that everything was built properly, you should see:
> ========== Build: 3 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========

in the output console at the bottom and all of these 3 .exe:

* topaz_connect.exe
* topaz_game.exe
* topaz_search.exe

should be present in the \topaz\ folder.

## 5. Server configuration:

In the \topaz\conf folder, open these three files (with the default Windows text editor (Notepad) or an external one (like  [Notepad++](https://notepad-plus-plus.org/)):

* login.conf
* map.conf
* search_server.conf

then modify this line each time:

> mysql_password: root 

(replace "root" with your MariaDB password)

Servers are now configured properly. Execute all the following .exe located in the \topaz\ folder (as Admin):

* topaz_connect.exe
* topaz_game.exe
* topaz_search.exe (optional, to use the search function)

/!\ **DirectPlay** /!\

You may need to enable this feature to make things work:
Start menu > Windows System > Control Panel > Programs and Features > Turn Windows features on or off:
Open "Legacy Components" and check "DirectPlay" > OK.

## 6. How to update the server:

1. Right click wherever you want > TortoiseGit > Settings > Context Menu > check: "Pull..." > Apply > OK.

2. Right click on the "topaz" folder > Git Pull... > Remote Branch: (select or type) "release" (stable) or "canary" (master) > OK > Close.

By looking at the files that were changed, you should:

* RERUN EVERY .sql MODIFIED FILES (referring to the example at **3. 2.**).
* REBUILD THE SOLUTION IF ANY .cpp/.h/.in IS MODIFIED (referring to the whole example at **4.**).
* RESTART YOUR SERVER(S) FOR .conf FILES.
* .lua files ARE INSTANT
---

If any new .py file is added (in \topaz\migrations\) during an update make sure to:
1. Install [MySQL Connector Python](https://dev.mysql.com/downloads/connector/python/).
2. Execute the migrate.py file in there to apply possible changes.

---

When an official update is available, you'll need to update the client (Final Fantasy) too. Repeat the whole process listed in step [2. Updating (automatic way) Client installation setup guide](https://github.com/project-topaz/topaz/wiki/Client-installation-setup-%5BWindows-10%5D).

/!\ **common issues** /!\

If the server (Project Topaz) and the client (Final Fantasy XI) don't share the same version, you'll probably get this error in the topaz_connect.exe log window:

```
[Error] lobbyview_parse: Incorrect client version: got 000000xx_x, expected 000000xx_x
[Error] lobbyview_parse: The server must be updated to support this client version
```

Open the topaz\version.info file with a text editor (Notepad or [Notepad++](https://notepad-plus-plus.org/)) and modify the following line:

> ENABLE_VER_LOCK: 1 

to

> ENABLE_VER_LOCK: 0

save then restart the topaz_connect.exe server.

## 7. Save your database

_Exporting_:

1. Execute HeidiSQL > select your session and connect to it > select "tpzdb" in the left panel > select:
```
accounts
auction_house
chars
char_effects
char_equip
char_exp
char_inventory
char_jobs
char_look
char_pet
char_points
char_profile
char_skills
char_spells
char_stats
char_storage
char_vars
conquest_system
delivery_box
linkshells
```
2. Right click on it/them > Export database as SQL...:
```
Table(s): check "Create".
Data: Insert.
Output: Directory - one file per object in database subdirectories.
Directory: (click on the folder icon on the right then choose a name and a location to save your stuff).
```
3. Export > Close.

_Importing_:

Repeat the whole process of the **3. 2.** part (but select the .sql files you saved before instead).

---

## Miscellaneous

If you can hear ambient sound (music, weather, etc.) but no sound effects, this is one of the possible fixes:

Right click on Speakers > Sounds > Playback tab > right click on Speakers > Configure Speakers > select Stereo > Next > Next > OK.

---

For gil not sent to the Delivery Box (from the Auction House), this is one of the possible fixes:

Execute HeidiSQL > select your session and connect to it > select "tpzdb" > File > Run SQL file... > select the triggers.sql file from the \topaz\sql folder > Open.

---

Local macros location: PlayOnline\SquareEnix\FINAL FANTASY XI\USER.

_Official_ screenshots location: PlayOnline\SquareEnix\PlayOnlineViewer\pub\home01\ open\ScreenShots\FinalFantasyXI.

---

Make your character a Game Master:

Execute HeidiSQL > connect to your database > select "chars" > "Data" tab > "gmlevel" column > modify the value from 0 to 5 (maximum level) > close HeidiSQL.

Change zone in game to apply.

Type "!command" in game (refer to the \topaz\scripts\commands folder for a list of commands).

!togglegm: no more aggro.
!togglegm + /anon: invisible through /search.
!hide: invisible to players.

---

How to change your loader password:

Execute HeidiSQL > select your session and connect to it > select "tpzdb" > select the "accounts" table > "Query" tab > enter the following line:
```
update accounts set password = password('Your.new.password') where id=Your.account.ID
```
Click on "Execute SQL... (F9)" > Yes.

/!\ **issue regarding the length of the password** /!\ 

It is possible to change your password if the _new one_ doesn't exceed 16 characters. If that's the case, the query will be taken in consideration but **you won't be able to log in through the loader**.
It is possible to have a password that exceeds 16 characters but _only_ when you create your account through the loader.
