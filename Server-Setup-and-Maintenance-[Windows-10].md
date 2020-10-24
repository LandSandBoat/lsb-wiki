### ⚠️ IF YOU HAVEN'T ALREADY CONFIGURED A CLIENT TO CONNECT TO A PRIVATE SERVER, FOLLOW THIS ONCE YOU'RE _DONE_ WITH THIS FIRST PART: [[Client Setup [Windows]|https://github.com/project-topaz/topaz/wiki/Client-setup-%5BWindows%5D]]

## 1. Software needed:

### ⚠️ Make sure you have the latest version of each software mentioned on this page installed on your system, and only this one

To build, run, and maintain a Topaz server, you will need to download and install the following third-party software:

**All of:**
* [Git for Windows](https://gitforwindows.org/): Accept defaults.
* [Visual Studio Community 2019](https://visualstudio.microsoft.com/vs/community/): Under "Workloads" > check "Desktop development with C++". Creating/linking a free account may be required to use it. Used to compile and build the source files.
* [MariaDB](https://mariadb.org/): Includes HeidiSQL GUI frontend for viewing and editing your SQL database, just remember the password you set for MariaDB during the installation. Used as SQL database. _**New versions of MySQL from Oracle will NOT work. Use MariaDB!** MySQL hasn't worked properly out of the box since 5.7 - that's a long time ago!_
* [Python](https://www.python.org/downloads/): **Must be 3.5+, _not_ 2.7!** Check "Add Python 3.8 to PATH". Click on "Customize installation" then everything should be checked on the first window that shows up > Next. Options 2, 3 and 4 should be checked on the second window. Install > Close. Make sure .py files are associated with Python by default so you can double click on them to open them.

**Optional:**
* [GitHub Desktop](https://desktop.github.com/), a Git GUI for managing git repositories and branches.
* [TortoiseGit](https://tortoisegit.org/), a Git GUI for managing git repositories and branches.


## 2. Download the source code:
<details>
  <summary>Git CLI</summary>
  
1. Open a PowerShell window.
2. Type:
```
git clone --recursive https://github.com/project-topaz/topaz.git
```
</details>
<details>
  <summary>GitHub Desktop</summary>
  
1. Open GitHub desktop. File > Clone repository > URL button (along top).
2. Enter the following:
  * Repository URL: either [your forked copy of our repository](https://raw.githubusercontent.com/wiki/project-topaz/topaz/images/github-fork.png) `https://github.com/your-github-name/topaz.git` (recommended), or our repository `https://github.com/project-topaz/topaz.git`
  * Local path: Where you want the source code to live on your computer.
3. Select `Clone` button:
[[/images/github-desktop-clone.png|Pull Origin button location]]
</details>
<details>
  <summary>TortoiseGit</summary>
  
1. Right click wherever you want to download the repository > Git Clone... > URL: https://github.com/project-topaz/topaz.git ("release" branch by default) > OK > then Close when it's done. 

2. Don't forget about Navmeshes (https://github.com/project-topaz/xiNavmeshes.git): right click on the freshly downloaded "topaz" folder > TortoiseGit > Submodule Update... > OK > then Close when it's done.
</details>

## 3. .conf files configuration:

In the `topaz\conf\default\` folder, make sure you **copy** all the files in there and put them in the precedent folder (`topaz\conf\`) like the readme.md file says. Open these three files (with the default Windows text editor (Notepad) or an external one (like  [Notepad++](https://notepad-plus-plus.org/)):

* login.conf
* map.conf
* search_server.conf

then modify this line each time:

> mysql_password: root 

(replace "root" with your MariaDB password)

## 4. Preparing the database:

In the `topaz\tools\` folder, right click + holding the Shift key > context menu: Open command window here/Open PowerShell window here.: then type:

```
py -3 -m pip install -r requirements.txt
```
It will download and install MySQL Connector Python, gitpython, pyyaml, colorama and pip.

Followed by:
```
py -3 dbtool.py
```
(or just double click on `topaz\tools\dbtool.py`)

In the new dbtool window:

"Database tpzdb (default name, change it in the .conf files if you want a different one) does not exist. Would you like to create new database: tpzdb? [y/N]" > y > Enter

Done.

If you are running a server for others to connect to, you NEED to update the `zoneip` column in the `zone_settings` table in your database. An easy way to do this is to create a .sql file in `topaz\sql\backups\` with the following line: 
```
UPDATE zone_settings SET zoneip = 'your.public.IP';
```
Then run dbtool, select the option to Restore/Import, and import the file you just created. Be sure to import this file again if an update overwrites this setting. You can also use a url as the zoneip, as in: 
```
UPDATE zone_settings SET zoneip = 'myurl.noip.com';
```
This process is also how you would go about maintaining custom mob levels, positions, and other custom database changes while staying mostly up to date with upstream.

---
⚠️

Updating Python: Default location of the Python installation files is: `C:\Users\Username\AppData\Local\Programs\Python`, when updating you may want to relocate old files from your old version's folder to the new one (copy/paste).

Updating modules: Make sure you check if your modules are up to date from time to time (you'll probably get reminded while running migrations scripts). To do so, open a command prompt like stated above and enter:
```
py -3 -m pip install --upgrade Modulename
```

## 5. Build the servers:

**We have a new build system, read how to use it here:**

https://github.com/project-topaz/topaz/wiki/CMake-Build-Guide

* topaz_connect.exe
* topaz_game.exe
* topaz_search.exe

should be present in the `topaz\` folder.

Servers are now configured properly. Execute all the above .exes (as Administrator, you can create a shortcut for each one and topaz_search.exe is optional, if you want to use the search function and pydarkstar).

---

⚠️ **Port forwarding**

If you are running a server for others to play on, make sure you have the following ports forwarded:

TCP ports: 54230, 54231, 54001 and 54002.

UDP port: 54230.

---

⚠️ **Common Issue**

⚠️ **WE STRONGLY ADVISE AGAINST LOCKING THE SERVER TO OLDER VERSIONS. IT IS A UNIVERSALLY BAD IDEA.** It _will_ cause issues even _if_ you manage to keep both server and client versions on par!

If the server (Project Topaz) and the client (Final Fantasy XI) don't share the same version, you'll probably get this error in the topaz_connect.exe log window:

```
[Error] lobbyview_parse: Incorrect client version: got 000000xx_x, expected 000000xx_x
[Error] lobbyview_parse: The server must be updated to support this client version
```

Open the `topaz\conf\version.conf` file with a text editor (Notepad or [Notepad++](https://notepad-plus-plus.org/)) and modify the following line:

> VER_LOCK: 2

to:

> VER_LOCK: 0

save then restart the topaz_connect.exe server.

