 I will not be covering how to set up a Raspberry Pi with [NOOBs](https://www.raspberrypi.org/downloads/noobs/) or Raspbian in this guide, as this is covered in many places on the Internet.  This guide assumes basic knowledge of Raspbian, terminal commands, and the raspberry pi limitations.

All the steps below in code block are to be done on the terminal unless otherwise noted:

## Getting the files

Install the requirements to run the sql database, tools to compile the source code, and lua.
```
sudo apt update
sudo apt install mariadb-server-10.0 libmariadb-dev-compat libluajit-5.1-dev libzmq3-dev liblua5.1-bitop autoconf pkg-config
```

Clone the repository to a new folder named topaz by putting:
```
git clone --recursive https://github.com/project-topaz/topaz.git
```

## Compiling the Server

Go inside the project's folder and compile the source code like so:
```
cd topaz
sh autogen.sh
./configure --enable-debug=gdb
make -j $(nproc)
```
You will get some warnings with configure, as long as there are no FATAL errors, you're ok to continue.  
Note 1: if you aren't debugging your server, you can replace ```./configure --enable-debug=gdb``` with just ```./configure```  
Note 2: ```$(nproc)``` is a system variable for the number of processor cores you have.  You can just do ```make``` if you only want to use 1, or change ```$(nproc)``` to a number to use however many cores manually.  Due to an issue with the Raspberry pi reporting incorrect hardware information, I strongly advise you to either just use make, or manually identify your number of cores!  Using ```-j $(nproc)``` crashed my Pi (3b).  If you just use make, your pi may take a while to do this on a 3b/3b+ (not sure with a 4b as I currently don't have access to one)

You may get an error like:
```
topaz_game-instance_loader.o: undefined reference to symbol 'pthread_create@@GLIBC_2.4'
```
If you do, do configure again like this
```
./configure CXXFLAGS="-pthread"
```
and then run make again.

## Setting up the Database
Next, we want to remove remote root access to the database, and set a secure password.  Run:
```
sudo mysql_secure_installation
```
and you will get prompted for a password.  If you've been following this guide exactly and did not have mysql/mariadb set up prior, just press enter.  If it says access denied, you likely forgot sudo.  It will go through a series of questions, to which you want to type Y and enter to all of them, and set a secure password to root when asked (second question).  This will also remove test tables you wont need, and anonymous account access.

Next, log into your DB as root with:
```
sudo mysql -u root -p
```

Create a user.  This example creates user 'topazadmin' with the password 'topazisawesome' that can only connect via localhost (the computer the db is on).  To connect via a specific network or IP address, replace local host with the correct IP address you'll be connecting from.  To connect via any IP address, replace localhost with % (i.e. 'topazadmin'@'%')... make absolutely certain you use a **secure** password if you do this!
```
CREATE USER 'topazadmin'@'localhost' IDENTIFIED BY 'topazisawesome';
```

Create the tpzdb database and grant all access to the user we just created (topazadmin)
```
CREATE DATABASE tpzdb;
USE tpzdb;
GRANT ALL PRIVILEGES ON tpzdb.* TO 'topazadmin'@'localhost';
exit
```
This **must** match the user you created above, including the @'ipaddress' part, or you wont have permissions to do anything.

If you did not create a user for a remote computer, or a user@'%', you will need to upload the sql files to the DB still on the Raspberry Pi.

You can do this by doing (assuming you were still in the topaz folder in your terminal window):
```
cd sql
for f in *.sql
  do
     echo -n "Importing $f into the database..."
     mysql tpzdb -u topazadmin -ptopazisawesome < $f && echo "Success"      
  done
cd ..
```
For the for loop, you can use shift + enter to put it on multiple lines, once you type done and push enter (even if you're holding shift) it will process your loop.

## Get the server ready to run

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

Next, copy these config files from conf/default to the conf folder:
```
cp conf/default/* conf/
```

Now we are going to enter the username and password for sql inside three different files login.conf, map.conf, and search_server.conf
For each of these, there will be a line that says ```mysql_login``` and mysql_password```.

You want to change them so that they match the username and password you created to log in to your DB.  For example from
```
mysql_login: root
mysql_password: root
```
to
```
mysql_login: TheBoss
mysql_login: n0t4R3a1Pw
```
Once you enter a nano command, you'll be presented with the text in the file.  When you've made your changes, press Ctrl + X on your keyboard, then Y, and then enter to save and quit, then enter the next command.
```
cd conf
nano login.conf
nano map.conf
nano search_server.conf
```
Note: map.conf has many options for controlling drop rates, exp rates, and other things you may want to change.

```
cd ..
```

For more settings you can change, you can use:
```
cd scripts/globals
nano settings.lua
```

If you ever get an error that prevents users from logging in that says "The client has been updated, plus log out and update your client through play online" or anything very similar to this, you'll need to edit version.info:
```
cd ../..
nano version.info
```
In this file, you can chenge the server version itself (make it match the intended client version, which you can find by logging into your client and typing /ver in chat).  You can also change the VER_LOCK: option to either not care at all(0) or allow clients that match the server version, and newer versions, to connect (2).  Note an either case, if the user's client version does not match the version in this file, the player will be presented with a message that says "This server does not support this client."  Most of the time, this is nothing to worry about, but if there is a version that has major differences, players may receive weird functionality or even crashes caused by incorrect data being sent between the server and the client.  It is recommended that your players use a client version that is as close to your server version as possible.

## Running your server

Now for running the server, we have a couple of options.  If your running xwindows (desktop ui like Windows) you can double click the 3 server files topaz_connect, topaz_game, and topaz_search.  You will get presented with a prompt asking you how you want to run them, pick Execute in terminal or they will run in the background.  By default, they will not have a file extension (this is completely normal if you're not used to Linux).


Or you can try this:
```
screen -d -m -S topaz_connect ./topaz_connect
screen -d -m -S topaz_game ./topaz_game
screen -d -m -S topaz_search ./topaz_search
```
Which is a linux equivalent of running the server in the background.  If you choose this route, and you need to see the output for some reason you can use:
```
screen -r topaz_connect
screen -r topaz_game
screen -r topaz_search
```

If for some reason that doesn't work, you can also use:
```
journalctl -u topaz_game.service -b
journalctl -u topaz_connect.service -b
journalctl -u topaz_search.service -b
```

## Shutdown the server
If you've run them in a terminal by double click, or using ```./topaz-x``` in the terminal, just click that terminal window and hit Ctrl+C on your keyboard, or click the X.  If you've run them using the screen commands, you'll have to do this instead:
```
sudo systemctl stop topaz_connect
sudo systemctl stop topaz_game
sudo systemctl stop topaz_search
```

Please, make sure you're players are logged out before shutting down your servers!


That's everything about basic setup for the server.  If you get any errors not handled by this guide, please head over to the #troubleshooting channel on the discord for Topaz, and let us know what you did, and what error you're getting so we can help you resolve it, or head over to #general and let us know how it went for you.


## Warnings
#### RAM
The Raspberry pi 3b/3b+ only has 1GB of ram, and it only has access to a certain amount which varies based on how much you set aside for your graphics adapter during the initial set up of your pi.  Due to this, running topaz_game my make your pi seemingly freeze.  It is thusly advised that you run your servers one at a time starting with topaz_connect, then topaz_game, then topaz_search until they all say they are ready (the search one is the fastest, it will pretty much be ready as soon as it's run).  However, once topaz_game has done everything it needs to do and has run for a certain amount of time aftwards, it will only use about 250MB by itself, adding about 1.5MB give or take for additional players, and the other 2 servers use very little.  It is recommended, for this reason, that you disable areas you are not going to use on your server.  This can be done by changing the IP address of the zones in zone_settings in your database, or removing the zone from zone_settings.  You can also cluster zones to different machines, and use other Pis or computers to host them.
#### Power
Raspberry Pis require at least a 2.5amp power supply to run at full power, if you are getting a little yellow lightning bolt in the top right, you have hit the limit of your current power supply, and may not be able to take full advantage of your CPU's power, and may lose connectivity to Bluetooth, or USB devices.

Should you hit either of these 2 limitations, it will take considerably longer for the process to finish, my Pi 3b ran for 12 hours and never finished loading all the zones and reducing the RAM usage to normal ranges.