This is the wiki for Project Topaz. As we are still setting up the project, it may be sparse until more work is put into it.

## Server Installation + Setup

(For Windows 10.)

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

# Server Installation + Setup [Ubuntu 18.04 LTS]

All the steps below in code block are to be done on the terminal:

Installs requirements to run the sql database and tools to compile the source code
```
sudo apt update
sudo apt install mysql-server libmysqlclient-dev libluajit-5.1-dev libzmq3-dev autoconf pkg-config
```

Clones the repository to the current folder you are in
```
git clone --recursive https://github.com/project-topaz/topaz.git
```

Goes inside the project's folder and compiles the source code
```
cd topaz
sh autogen.sh
./configure --enable-debug=gdb
make -j $(nproc)
```

The following command sets up mysql (Follow the prompts)
We won't be using the root account for the database we will be using
Root password: "Choose a secure root password"
Remove annonymous user: yes
Disallow root login: yes
Remove test data: yes
Reload privileged data: yes
```
sudo mysql_secure_installation
```

Logs in to sql
```
sudo mysql -u root -p
```

Creates the user 'topazadmin' with the password 'topazisawesome'
```
CREATE USER 'topazadmin'@'localhost' IDENTIFIED BY 'topazisawesome';
```

Creates the tpzdb database and grants all access to the user we just created (topazadmin)
```
CREATE DATABASE tpzdb;
USE tpzdb;
GRANT ALL PRIVILEGES ON tpzdb.* TO 'topazadmin'@'localhost';
exit
```

Goes inside the sql folder and imports all tables inside the database we just created (tpzdb)
```
cd sql
for f in *.sql
  do
     echo -n "Importing $f into the database..."
     mysql tpzdb -u topazadmin -ptopazisawesome < $f && echo "Success"      
  done
cd ..
```

Run the following command if your server is going to be available to the whole internet, to get your IP address.
Keep a record of this IP address
```
dig TXT +short o-o.myaddr.l.google.com @ns1.google.com | awk -F'"' '{ print $2}'
```

Run the following command if your server is only going to be available to machines at your home
Keep a record of this IP address
```
hostname -I
```

The following is going to log in to your sql server and change the zoneip value of the zone_settings table
Replace '127.0.0.1' with the IP you will be using from the previous step
```
mysql -u topazadmin -ptopazisawesome
USE tpzdb;
UPDATE zone_settings SET zoneip = '127.0.0.1'; 
exit
```

Now we are going to enter the username and password for sql inside three different files login.conf, map.conf, and search_server.conf
```
cd conf
nano login.conf
```
Look for mysql_login: root and change it to mysql_login: topazadmin
Look for mysql_password: root and change it to mysql_password: topazisawesome
Once that's changed press CONTROL + X, then press enter and hit Y to save the file
```
nano map.conf
```
Look for mysql_login: root and change it to mysql_login: topazadmin
Look for mysql_password: root and change it to mysql_password: topazisawesome
Once that's changed press CONTROL + X, then press enter and hit Y to save the file
```
nano search_server.conf
```
Look for mysql_login: root and change it to mysql_login: topazadmin
Look for mysql_password: root and change it to mysql_password: topazisawesome
Once that's changed press CONTROL + X, then press enter and hit Y to save the file
```
cd ..
```

For any custom changes you need to make to your server
```
cd scripts/globals
nano settings.lua
```

For any change to the version you want your clients be running
```
cd ../..
nano version.info
```

Now it's time to run your server
```
screen -d -m -S topaz_connect ./topaz_connect
screen -d -m -S topaz_game ./topaz_game
screen -d -m -S topaz_search ./topaz_search
```

You are done :)

If you need to connect to one of those three screens we have created to take a look at the logs run
```
screen -r topaz_connect
screen -r topaz_game
screen -r topaz_search
```

## Client Setup
How to set up a client to connect to a Project Topaz server
## Documentation
Information for developers who code for Project Topaz
## [Project Meta](https://github.com/project-topaz/topaz/wiki/Project-Meta)
Information relating to the "meta" of Project Topaz - like project goals, codes of conduct, project roadmaps, and licensing information
## Resources
Additional resources and tools of interest to administrators, developers, or players