### /!\ NEXT STEP TO FOLLOW ONCE YOU'RE _DONE_ WITH THIS FIRST PART: [[Client Setup [Windows]|https://github.com/project-topaz/topaz/wiki/Client-setup-%5BWindows%5D]] /!\

## 1. Software needed:

### /!\ Make sure you have the latest version of each software mentioned on this page installed on your system, and only this one /!\

To build, run, and maintain a Topaz server, you will need to download and install the following third-party software:

**All of:**
* [Git for Windows](https://gitforwindows.org/): Accept defaults.
* [Visual Studio Community 2019](https://visualstudio.microsoft.com/vs/community/): Under "Workloads" > check "Desktop development with C++". Creating/linking a free account may be required to use it. Used to compile and build the source files.
* [MariaDB](https://mariadb.org/): You can install HeidiSQL from there or get it separately, just remember the password you set for MariaDB during the installation. Used as SQL database. _**New versions of MySQL from Oracle will NOT work. Use MariaDB!** MySQL hasn't worked properly out of the box since 5.7 - that's a long time ago!_
* [HeidiSQL](https://www.heidisql.com/): Accept defaults. Used as a GUI frontend for viewing and editing your SQL database.
* [Python](https://www.python.org/downloads/): **Must be 3.5+, _not_ 2.7!** Check "Add Python 3.8 to PATH". Click on "Customize installation" then everything should be checked on the first window that shows up > Next. Options 2, 3 and 4 should be checked on the second window. Install > Close. Make sure .py files are associated with Python by default so you can double click on them to open them.
* [MySQL Connector Python](https://dev.mysql.com/downloads/connector/python/): Accept defaults (it will be installed through Python below if you don't want to download it this way).

**Make sure both Python and the MySQL Connector are x86 or x64**.

**One of:**
* [GitHub Desktop](https://desktop.github.com/), a Git client for managing git repositories and branches.
* [TortoiseGit](https://tortoisegit.org/), a Git client for managing git repositories and branches.


## 2. Download the source code:

**GitHub Desktop:**
1. Open GitHub desktop. File > Clone repository > URL button (along top).
2. Enter the following:
  * Repository URL: either [your forked copy of our repository](https://raw.githubusercontent.com/wiki/project-topaz/topaz/images/github-fork.png) `https://github.com/your-github-name/topaz.git` (recommended), or our repository `https://github.com/project-topaz/topaz.git`
  * Local path: Where you want the source code to live on your computer.
3. Select `Clone` button:
[[/images/github-desktop-clone.png|Pull Origin button location]]

**TortoiseGit:**
1. Right click wherever you want to download the repository > Git Clone... > URL: https://github.com/project-topaz/topaz.git ("release" branch by default) > OK > then Close when it's done. 

2. Don't forget about Navmeshes (https://github.com/project-topaz/xiNavmeshes.git): right click on the freshly downloaded "topaz" folder > TortoiseGit > Submodule Update... > OK > then Close when it's done.

## 3. .conf files configuration:

In the \topaz\conf\default folder, make sure you take all the files in there and put them in the precedent folder (\topaz\conf\) like the readme.md file says. Open these three files (with the default Windows text editor (Notepad) or an external one (like  [Notepad++](https://notepad-plus-plus.org/)):

* login.conf
* map.conf
* search_server.conf

then modify this line each time:

> mysql_password: root 

(replace "root" with your MariaDB password)

## 4. Preparing the database:

Right click + holding the Shift key > context menu: Open command window here/Open PowerShell window here.: then type (**use "pip3" (default) or "pip" in each command, the one that works for you**):

```
py -m pip3
```
enter this command:
```
pip3 install -r requirements.txt
```

then type this command (hit "Enter" right after):

```
py -m pip3 install pip
```
It will download and install MySQL Connector Python, gitpython, pyyaml, colorama and pip.

Followed by:
```
py dbtool.py
```
(or just double click on \topaz\tools\dbtool.py)

In the new dbtool window:

"Database tpzdb (default name, change it in the .conf files if you want a different one) does not exist. Would you like to create new database: tpzdb? [y/N]" > y > Enter > Done.

Run HeidiSQL > enter your MariaDB password > verify that the IP address displayed in the "zoneip" column ("Data" tab) of the zone_settings table (bottom) is the correct one (local (127.0.0.1) by default). If you are running a server for others to connect to, you NEED to update this setting. You can adjust all the lines at once by clicking on the "Query" tab then typing:

  > UPDATE zone_settings SET zoneip = '**your.IP**';

  Click on "Execute SQL..." (blue icon on top) > Yes.

---
/!\

Updating Python: Default location of the Python installation files is: C:\Users\Username\AppData\Local\Programs\Python, when updating you may want to relocate old files from your old version's folder to the new one (copy/paste).

Updating modules: Make sure you check if your modules are up to date from time to time (you'll probably get reminded while running migrations scripts). To do so, open a command prompt like stated above and enter:
```
py -m pip3 install --upgrade Modulename
```

## 5. Build the servers:

1. Execute Visual Studio Community 2019: Open a project or solution (on the right) > select the "topaz.sln" file from the \topaz\win32 folder > Open.

2. Once it's loaded > Build > Build Solution.

3. To confirm that everything was built properly, you should see:
> ========== Build: 3 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========

in the output console at the bottom and all of these 3 .exe:

* topaz_connect.exe
* topaz_game.exe
* topaz_search.exe

should be present in the \topaz\ folder.

Servers are now configured properly. Execute all the above .exes (as Administrator, you can create a shortcut for each one and topaz_search.exe is optional, if you want to use the search function and pydarkstar).

---

/!\ **Port forwarding** /!\

If you are running a server for others to play on, make sure you have the following ports forwarded:

TCP ports: 54230, 54231, 54001 and 54002.

UDP port: 54230.

## 6. How to update the server:
**GitHub Desktop:**
1. Open GitHub Desktop. Next to where your current branch is listed, click either `Fetch origin` (checking for updates), or `Pull origin`
[[/images/pull_origin.png|Pull Origin button location]]

**TortoiseGit:**
1. Right click wherever you want > TortoiseGit > Settings > Context Menu > check: "Pull..." > Apply > OK.

2. Right click on the "topaz" folder > Git Pull... > Remote Branch: (select or type) "release" (stable) or "canary" (master) > OK > Close.

By looking at the files that were changed, you should:

* RERUN EVERY .sql MODIFIED FILES: double click on \topaz\tools\dbtool.py > select "e. Express Update" (available if .sql were changed) > Enter > "Would you like yo backup your database? [y/N]" > y > Enter > "Proceed with update? [y/N] > y > Enter > Done. This will run all your .sql files. It will also possibly overwrite any custom changes you have made to your SQL tables. If you are running custom mobs/items/etc. of any kind, you'll want to load the SQL changes to a separate database and compare.
* REBUILD THE SOLUTION IF ANY .cpp/.h/.in IS MODIFIED (referring to the whole example at **[5. Build the servers](https://github.com/project-topaz/topaz/wiki/Server-Setup-and-Maintenance-%5BWindows-10%5D/_edit#5-build-the-servers)**).
* RESTART YOUR SERVER(S) FOR .conf FILES.
* .lua files ARE INSTANT IN MOST CASES (\topaz\scripts\globals .luas will need to be reloaded by using the GM command !reloadglobal where appropriate or restarting the server).
* If there's any new .py file addition in the \topaz\tools\migrations folder, double click on \topaz\tools\dbtool.py > select "e. Express Update" (available if .py scripts were changed) > Enter > "Would you like yo backup your database? [y/N]" > y > Enter > "Proceed with update? [y/N] > y > Enter > Done. This will run all your .py migrations scripts.
* /!\ In the \topaz\conf\default folder, make sure you take any .conf file that was updated and put it/them in the precedent folder (\topaz\conf). /!\

---

When an official update is available, you'll need to update the client (Final Fantasy) too. Repeat the whole process listed in step [2. Updating (automatic way) Client installation setup guide](https://github.com/project-topaz/topaz/wiki/Client-installation-setup-%5BWindows-10%5D).

/!\ **common issue** /!\

/!\ **WE STRONGLY ADVISE AGAINST LOCKING THE SERVER TO OLDER VERSIONS. IT IS A UNIVERSALLY BAD IDEA.** It _will_ cause issues even _if_ you manage to keep both server and client versions on par! /!\

If the server (Project Topaz) and the client (Final Fantasy XI) don't share the same version, you'll probably get this error in the topaz_connect.exe log window:

```
[Error] lobbyview_parse: Incorrect client version: got 000000xx_x, expected 000000xx_x
[Error] lobbyview_parse: The server must be updated to support this client version
```

Open the topaz\conf\version.conf file with a text editor (Notepad or [Notepad++](https://notepad-plus-plus.org/)) and modify the following line:

> VER_LOCK: 2

to:

> VER_LOCK: 0

save then restart the topaz_connect.exe server.

## 7. Database management

Execute \topaz\tools\dbtool.py.

_Backup_:

Select "3. Backup" > Enter > "Would you like to backup your database? [y/N]" > y > Enter > Done.

_Restore/Import_:

Select "4. Restore/Import" > Enter > "Would you like to backup your database? [y/N]" > y > Enter > "Choose a number to import, or type "delete #" to delete a file." > select desired backup > Enter > "If this is a full backup created by this tool, it is recommended to manually change the DB_VER in ..\conf\version.conf to the hash sequence in the filename, between the database name and the timestamp, so that express update functions properly. Import _desired-backup.sql_? [y/N]" > y > Enter > Done.

/!\

```
  - accounts.sql
  - accounts_banned.sql
  - auction_house.sql
  - char_blacklist.sql
  - char_effects.sql
  - char_equip.sql
  - char_exp.sql
  - char_inventory.sql
  - char_jobs.sql
  - char_look.sql
  - char_merit.sql
  - char_pet.sql
  - char_points.sql
  - char_profile.sql
  - char_skills.sql
  - char_spells.sql
  - char_stats.sql
  - char_storage.sql
  - char_style.sql
  - char_unlocks.sql
  - char_vars.sql
  - chars.sql
  - conquest_system.sql
  - delivery_box.sql
  - linkshells.sql
  - server_variables.sql
```
These files will be left untouched during updates and partial backups of the database. You can manually edit them in \topaz\tools\config.yaml.