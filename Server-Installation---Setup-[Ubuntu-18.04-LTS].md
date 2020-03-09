All the steps below in code block are to be done on the terminal:

Installs requirements to run the sql database and tools to compile the source code
```
sudo apt update
sudo apt install mariadb-server libmariadbclient-dev libluajit-5.1-dev libzmq3-dev autoconf pkg-config
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