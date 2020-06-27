## 1. Software needed:

### /!\ Make sure you have the latest version of each software mentioned on this page installed on your system, and only this one /!\

To build, run, and maintain a Topaz server, you will need to download and install the following third-party software:

**All of:**
* [Visual Studio Community 2019](https://visualstudio.microsoft.com/vs/community/): Under "Workloads" > check "Desktop development with C++". Creating/linking a free account may be required to use it. Used to compile and build the source files.
* [MariaDB](https://mariadb.org/): You can install HeidiSQL from there or get it separately, just remember the password you set for MariaDB during the installation. Used as SQL database. _**New versions of MySql from oracle will NOT work. Use MariaDB!** MySql hasn't worked properly out of the box since 5.7 - that's a long time ago!_
* [HeidiSQL](https://www.heidisql.com/): Accept defaults. Used as a GUI frontend for viewing and editing your SQL database.
* [Python (latest version)](https://www.python.org/downloads/): **Must be 3.5+, _not_ 2.7!** Accept defaults (make sure it's now the default application associated with .py files).  Used for server updates and migrations.

**One of:**
* [GitHub Desktop](https://desktop.github.com/), a git client for managing git repositories and branches
* [Git for Windows](https://gitforwindows.org/) _and_ [TortoiseGit](https://tortoisegit.org/), a git client for managing git repositories and branches


## 2. Download the source code:

**GitHub Desktop:**
1. Open GitHub desktop. File > Clone repository > URL button (along top)
2. Enter the following:
  * Repository URL: either [your forked copy of our repository](https://raw.githubusercontent.com/wiki/project-topaz/topaz/images/github-fork.png) `https://github.com/your-github-name/topaz.git` (recommended), or our repository `https://github.com/project-topaz/topaz.git`
  * Local path: Where you want the source code to live on your computer
3. Select `Clone` button
[[/images/github-desktop-clone.png|Pull Origin button location]]

**TortoiseGit:**
1. Right click wherever you want to download the repository > Git Clone... > URL: https://github.com/project-topaz/topaz.git ("release" branch by default) > OK > then Close when it's done. 

2. Don't forget about Navmeshes (https://github.com/project-topaz/xiNavmeshes.git): right click on the freshly downloaded "topaz" folder > TortoiseGit > Submodule Update... > OK > then Close when it's done.

## 3. Prepare the database:

1. Execute HeidiSQL and click on "New" (bottom left) then name your session as you wish > Password: Password previously saved from the MariaDB installation > Open > right click on the freshly created/named session (left) > Create new > Database > name it "tpzdb" > OK.

2. Run the Database_initial_setup.bat file located in the \topaz\tools folder. Alternatively, you can manually load files via this method: Select "tpzdb" > File > Run SQL file... > select every .sql file from the \topaz\sql folder > Open > click on "Refresh" (F5) once everything is done. 

3. Don't forget to verify that the IP address displayed in the "zoneip" column ("Data" tab) of the zone_settings table is the correct one (local (127.0.0.1) by default). If you are running a server for others to connect to, you NEED to update this setting. You can adjust all the lines at once by clicking on the "Query" tab then typing:

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

In the \topaz\conf\default folder, make sure you take all the files in there and put them in the precedent folder (\topaz\conf\) like the readme.md file says. Open these three files (with the default Windows text editor (Notepad) or an external one (like  [Notepad++](https://notepad-plus-plus.org/)):

* login.conf
* map.conf
* search_server.conf

then modify this line each time:

> mysql_password: root 

(replace "root" with your MariaDB password)

(If you have any problem with a mismatching version, check the /!\ **common issue** /!\ regarding updates below.)

Servers are now configured properly. Execute all the following .exe located in the \topaz\ folder (as Admin):

* topaz_connect.exe
* topaz_game.exe
* topaz_search.exe (optional, to use the search function)

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

* RERUN EVERY .sql MODIFIED FILES (referring to the example at **3. 2.**). This will overwrite any custom changes you have made to your sql tables. If you are running custom mobs/items/etc of any kind, you'll want to load the sql changes to a separate database and compare.
* REBUILD THE SOLUTION IF ANY .cpp/.h/.in IS MODIFIED (referring to the whole example at **4.**).
* RESTART YOUR SERVER(S) FOR .conf FILES.
* .lua files ARE INSTANT.
* RUN the migrate.py file if there's any new addition in the folder (see below).
* /!\ In the \topaz\conf\default folder, make sure you take the version.conf file and put it in the precedent folder (\topaz\conf) after a server update which include a Pull Request to be on par with the client (to prevent version error messages below). /!\
---

If any new .py file is added (in \topaz\migrations\) during an update make sure to:
1. Download and install [MySQL Connector Python](https://dev.mysql.com/downloads/connector/python/): Accept defaults.
2. Make sure your .conf files are out of the default folder and have the correct passwords entered to access your database.

* Python script way:

Double click on the migrate.py script in the \topaz\migrations folder.

* Command prompt way (**use "pip3" (default) or "pip" in each command, the one that works for you**):

Right click + holding the Shift key in the \topaz\migrations folder (empty space, not a file) > context menu: Open command window here/Open PowerShell window here.
(skip this step if you installed the MySQL Connector Python above) enter this command:
```
pip install -r requirements.txt
```
or
```
pip3 install mysql-connector-python
```
It will download and install MySQL Connector Python.

5. Enter this command:
```
py migrate.py
```
It will run all the migrations scripts.

Updating Python: Default location of the Python installation files is: C:\Users\Username\AppData\Local\Programs\Python, when updating you may want to relocate old files from your old version's folder to the new one (copy/paste).

Updating modules: Make sure you check if your modules are up to date from time to time (you'll probably get reminded while running migrations scripts). To do so, open a command prompt like stated above and enter:
```
py -m pip3 install --upgrade Modulename
```

---

When an official update is available, you'll need to update the client (Final Fantasy) too. Repeat the whole process listed in step [2. Updating (automatic way) Client installation setup guide](https://github.com/project-topaz/topaz/wiki/Client-installation-setup-%5BWindows-10%5D).

/!\ **common issue** /!\

If the server (Project Topaz) and the client (Final Fantasy XI) don't share the same version, you'll probably get this error in the topaz_connect.exe log window:

```
[Error] lobbyview_parse: Incorrect client version: got 000000xx_x, expected 000000xx_x
[Error] lobbyview_parse: The server must be updated to support this client version
```

Open the topaz\conf\version.conf file with a text editor (Notepad or [Notepad++](https://notepad-plus-plus.org/)) and modify the following line:

> VER_LOCK: 2

to

> VER_LOCK: 0

save then restart the topaz_connect.exe server.

## 7. Database management

* Manual way:

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

* Automated way (thanks to Wren):

[.bat files (BACKUP - TPZ.bat and BUILD - TPZ.bat) + documentation](https://drive.google.com/open?id=1uqnmsABGWTMCCuLEN4jZtrv3OO0cWebs).

/!\

Don't forget to edit each one with a text editor and change paths accordingly first. There's a documentation guide in there to help out.

_Exporting_:

Download and execute the *BACKUP - TPZ.bat* one.

_Importing_:

Download and execute the *BUILD - TPZ.bat* one.