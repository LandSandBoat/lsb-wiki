##### Table of Contents  
- [Install](#install)  
- [Update](#update)  

# Install

All the steps below in code block are to be done on the terminal:

Installs requirements to run the sql database and tools to compile the source code
```
sudo apt update
sudo apt install cmake mariadb-server libmariadbclient-dev libmariadb-dev-compat libluajit-5.1-dev libzmq3-dev autoconf pkg-config zlib1g-dev libssl-dev
```
> Note: If you receive errors regarding dependency conflicts, you can remove `libmariadbclient-dev`


Clones the repository to the current folder you are in
```
git clone --recursive https://github.com/topaz-next/topaz.git
```

If you want to clone the repository with `canary` branch already checked-out you can use:
```
git clone --recursive --single-branch --branch canary https://github.com/topaz-next/topaz.git
```

Goes inside the project's folder and compiles the source code
```
cd topaz
mkdir build
cd build
cmake ..
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
cd ../sql
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
Replace '127.0.0.1' with the IP you will be using from the previous step - this is REQUIRED if your server is public-facing.
```
mysql tpzdb -u topazadmin -ptopazisawesome -e "UPDATE zone_settings SET zoneip = '127.0.0.1';" 
```

Now we are going to enter the username and password for sql inside three different files login.conf, map.conf, and search_server.conf

First, copy these config files to the conf folder:
```
cp conf/default/* conf/
```

Then edit them as follows:

```
cd conf
echo -e "\n#DB_VER: `git rev-parse --short=4 HEAD`" >> version.conf
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

Ubuntu installs with unatteded-upgrades enabled by default, this will cause issues
with mariadb restarting when an update is available, leaving the server without
access to the database. To fix this run
```
dpkg-reconfigure unattended-upgrades
```
and choose "No." You just have to make sure to run updates manually.


For any custom changes you need to make to your server
```
cd scripts/globals
nano settings.lua
```

For any change to the version you want your clients be running
```
cd ../..
nano conf/version.conf
```
Port forwarding 
```
If you are running a server for others to play on, make sure you have 
the following ports forwarded: 
TCP Ports: 54230 54231 54001 54002 UDP Port: 54230
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
**Next Step: [Post-Install Guide](https://github.com/topaz-next/topaz/wiki/Post-Install-Guide)**

# Update

As development is always ongoing, you may want to periodically update to the latest version of Topaz. This can be done quite simply with a few steps, and using the magic of `git`! 

1. Save your custom modifications + settings
```
git stash
```
This will ask git to store changes you've made since cloning so we can put them back after updating.
2. Pull new changes from the repository. You should also close your topaz servers before updating.
```
git pull origin release
```
This assumes you cloned from the topaz github as detailed above. If you are using your own fork, this command may differ for you.
3. Put back your changes
```
git stash pop
```
Git may notify you which, if any, files were changed by both yourself and the Topaz project. You will want to edit these to confirm they are set the way you'd like them.
4. Compile the source code
```
cd build
cmake ..
make -j $(nproc)
```
5. Run dbtool either with the TUI using `python3 dbtool.py` in the tools folder, or by running 
```
python3 dbtool.py update
```
If there is a SQL change detected, the TUI will give the option for an "express upgrade" and a chance to review the changes. The CLI option will automatically apply any changes if necessary, and has options (on by default) to backup the whole database first and to update the client version in `version.conf` if a version update happens.