First, pull updated server files from Project Topaz.
<details>
  <summary>Git CLI</summary>
  
1. In the `topaz\` folder, open a PowerShell window.
2. Type:
```
git stash
git pull
git stash pop
```
</details>
<details>
  <summary>GitHub Desktop</summary>
  
1. Open GitHub Desktop. Next to where your current branch is listed, click either `Fetch origin` (checking for updates), or `Pull origin`
[[/images/pull_origin.png|Pull Origin button location]]
</details>
<details>
  <summary>TortoiseGit</summary>
  
1. Right click wherever you want > TortoiseGit > Settings > Context Menu > check: "Pull..." > Apply > OK.

2. Right click on the "topaz" folder > Git Pull... > Remote Branch: (select or type) "release" (stable) or "canary" (master) > OK > Close.
</details>

After pulling the new files:



* RERUN EVERY .sql MODIFIED FILES: Open a PowerShell window in the `topaz\tools\` folder and type:
```
py -3 dbtool.py update
```
This will import all of the .sql files that were updated and run any needed migrations. It will also possibly overwrite any custom changes you have made to your SQL tables. If you are running custom mobs/items/etc. of any kind, you'll want to save these as queries in a .sql file in `topaz\sql\backups\` and use the Restore/Import option in dbtool to import those changes after an update.

❔ For more information on database management, see [Database Management](https://github.com/project-topaz/topaz/wiki/Database-Management) or [Preparing the Database](https://github.com/project-topaz/topaz/wiki/Server-Setup-and-Maintenance-%5BWindows-10%5D/#4-preparing-the-database).

* REBUILD THE SOLUTION IF ANY .cpp/.h/.in IS MODIFIED (referring to the whole example at **[5. Build the servers](https://github.com/project-topaz/topaz/wiki/Server-Setup-and-Maintenance-%5BWindows-10%5D/#5-build-the-servers)**).
* RESTART YOUR SERVER(S) FOR .conf FILES AND AFTER UPDATES WITH dbtool.
* .lua files ARE INSTANT IN MOST CASES (`topaz\scripts\globals\` .luas will need to be reloaded by using the GM command `!reloadglobal` where appropriate or restarting the server).
* ⚠️ In the `topaz\conf\default\` folder, make sure you take any .conf file that was updated and put it/them in the precedent folder (`topaz\conf\`). Do not overwrite version.conf, as dbtool uses it to track DB version and will update CLIENT_VER for you if it changes. ⚠️