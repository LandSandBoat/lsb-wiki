## Softwares needed:

* Download and install [Visual Studio Community 2019](https://visualstudio.microsoft.com/vs/community/): Under "Workloads" > check "Desktop development with C++".
* Download and install [Git for Windows](https://gitforwindows.org/): Nothing to do in particular during the installation.
* Download and install [TortoiseGit](https://tortoisegit.org/): Nothing to do in particular during the installation.
* Download and install [MariaDB](https://mariadb.org/): You can install HeidiSQL from there or get it separately, just remember the password you set for MariaDB during the installation.
* Download and install [HeidiSQL](https://www.heidisql.com/): Nothing to do in particular during the installation.

## Download the source code:

* Right click wherever you want to download the repository > Git Clone... > URL: https://github.com/project-topaz/topaz.git > OK > then Close when it's done. 
* Don't forget about Navmeshes (https://github.com/project-topaz/xiNavmeshes.git): right click on the freshly downloaded "topaz" folder > TortoiseGit > Submodule Update... > OK > then Close when it's done.

## Prepare the database:

* Execute HeidiSQL and click on "New" (bottom left) then name your session as you wish > Password: Password previously saved from the MariaDB installation > Open > right click on it (left) > Create new > Database > name it "tpzdb" > OK.
* Select "tpzdb" > File > Run SQL file... > select every .sql files from the \topaz\sql folder > Open > click on "Refresh" (F5) once everything is done.

* Don't forget to verify that the IP adress displayed in the "zoneip" column ("Data" tab) of the zone_settings table is the correct one (local (127.0.0.1) by default). In case you need to update all the lines at once: Click on the "Query" tab the type:

> UPDATE zone_settings SET zoneip = '**your.IP**';

Click on "Execute SQL..." (blue icon on top) > Yes.

## Build the servers:

* Execute Visual Studio Community 2019: Open a project or solution (on the right) > select the "topaz.sln" file from the \topaz\win32 folder > Open.
* Once it's loaded > Build > Build Solution.

* To confirm that everything was built properly, you should see:
> ========== Build: 3 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========

in the output console at the bottom and all of these 3 .exe:

* topaz_connect.exe
* topaz_game.exe
* topaz_search.exe

should be present in the \topaz\ folder.

## Servers configuration:

In the \topaz\conf folder, open these three files (with the default Windows text editor (Notepad) or an external one (like  [Notepad++](https://notepad-plus-plus.org/)):

* login.conf
* map.conf
* search_server.conf

then modify this line each time:

> mysql_password: root (replace "root" with your MariaDB password)

Servers are now configured properly. Execute all the following .exe located in the \topaz\ folder (as Admin):

* topaz_connect.exe
* topaz_game.exe
* topaz_search.exe (optional, to use the search function)

/!\ DirectPlay /!\

You may need to enable this feature to make things work:
Start menu > Windows System > Control Panel > Programs and Features > Turn Windows features on or off:
Open "Legacy Components" and check "DirectPlay" > OK.