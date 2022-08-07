##### Table of Contents  
- [Install](#install)  
- [Update](#update)  
- [Miscellaneous](#miscellaneous)  

# Install

All the steps below in code block are to be done on the terminal:

Installs requirements to run the sql database and tools to compile the source code (click your distro)

<details>
  <summary>Debian/Ubuntu</summary>

```
sudo apt update
sudo apt install git python3 python3-pip g++-9 cmake make libluajit-5.1-dev libzmq3-dev libssl-dev zlib1g-dev mariadb-server libmariadb-dev
```
  * Note: Ubuntu 18.04 users will need to upgrade to g++-9.
    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt update
    sudo apt install g++-9
    ```
  * Note: Debian stable (Buster) users will need to install g++-9 from the testing branch.
    ```
    sudo echo 'deb http://deb.debian.org/debian testing main' > /etc/apt/sources.list.d/testing.list
    sudo apt update
    sudo cat <<EOF > /etc/apt/preferences.d/pin
    Package: *
    Pin: release a=stable
    Pin-Priority: 700

    Package: *
    Pin: release a=testing
    Pin-Priority: 650
    EOF

    sudo apt install -t testing g++-9
    ```

</details>
<details>
  <summary>Arch</summary>

```
sudo pacman -S git python3 python-pip gcc cmake make luajit zeromq openssl zlib mariadb
```
* Arch users will need to initialize and start the database software if not done already:
    ```
    sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
    sudo systemctl enable mariadb
    sudo systemctl start mariadb
    ```
</details>

Clone the repository to the current folder you are in
```
git clone --recursive https://github.com/LandSandBoat/server.git
```

If you want to clone the repository with `base` branch already checked-out you can use:
```
git clone --recursive --single-branch --branch base https://github.com/LandSandBoat/server.git
```

Go inside the project's folder and compile the source code
```
cd server
mkdir build
cd build
cmake ..
make -j $(nproc)
```
  * Note: If you had to upgrade to g++-9 it may be necessary to supply the compiler flag when using cmake.
    ```
    cmake -D CMAKE_CXX_COMPILER=g++-9 ..
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

Log in to sql
```
sudo mysql -u root -p
```

Create the user 'lsbadmin' with the password 'lsbisawesome'
```
CREATE USER 'lsbadmin'@'localhost' IDENTIFIED BY 'lsbisawesome';
```

Create the xidb database and grant all access to the user we just created (lsbadmin)
```
CREATE DATABASE xidb;
USE xidb;
GRANT ALL PRIVILEGES ON xidb.* TO 'lsbadmin'@'localhost';
exit
```

Go inside the sql folder and import all tables inside the database we just created (xidb)
```
cd ../sql
for f in *.sql
  do
     echo -n "Importing $f into the database..."
     mysql xidb -u lsbadmin -plsbisawesome < $f && echo "Success"      
  done
cd ..
```
Now we are going to enter the username and password for sql inside `network.lua`

First, copy the .lua settings files from the `settings\default\` folder to the `settings\` folder:
```
cp settings/default/* settings/
```

Then edit the copied `network.lua` as follows:

```
cd settings
echo -e "\n#DB_VER: `git rev-parse --short=4 HEAD`" >> network.lua
nano network.lua
```
Look for `SQL_LOGIN    = "root",` and change it to `SQL_LOGIN    = "lsbadmin",`

Look for `SQL_PASSWORD = "root",` and change it to `SQL_PASSWORD = "lsbisawesome",`

Once that's changed press CONTROL + X, then press enter and hit Y to save the file

NOTE: Any .lua files in the `settings\default\` folder that you wish to update needs to first be **copied** from the `server\settings\default\` folder and put in the precedent folder (`server\settings\`). Any .lua file(s) not updated can remain in the `server\settings\default\` folder (the .lua files in the `server\settings\default` folder are used if updated ones are not found in the `server\settings\` folder).

* Ubuntu installs with unattended-upgrades enabled by default, this will cause issues
with mariadb restarting when an update is available, leaving the server without
access to the database. To fix this run
  ```
  dpkg-reconfigure unattended-upgrades
  ```
  and choose "No." You just have to make sure to run updates manually.

Now it's time to run your server
```
cd ..
screen -d -m -S xi_connect ./xi_connect
screen -d -m -S xi_game ./xi_game
screen -d -m -S xi_search ./xi_search
```

You are done :)

If you need to connect to one of those three screens we have created to take a look at the logs run
```
screen -r xi_connect
screen -r xi_game
screen -r xi_search
```
**Next Step: [Post-Install Guide](Post-Install-Guide)**

# Update

As development is always ongoing, you may want to periodically update to the latest version of LandSandBoat. This can be done quite simply with a few steps, and using the magic of `git`! 

1. Save your custom modifications + settings
```
git stash
```
This will ask git to store changes you've made since cloning so we can put them back after updating.
2. Pull new changes from the repository. You should also close your topaz servers before updating.
```
git pull origin base
```
This assumes you cloned from the LSB github as detailed above. If you are using your own fork, this command may differ for you.
3. Put back your changes
```
git stash pop
```
Git may notify you which, if any, files were changed by both yourself and the LSB project. You will want to edit these to confirm they are set the way you'd like them.
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

# Miscellaneous
## Raspberry Pi Warnings
#### RAM
The Raspberry pi 3b/3b+ only has 1GB of ram, and it only has access to a certain amount which varies based on how much you set aside for your graphics adapter during the initial set up of your pi.  Due to this, running topaz_game my make your pi seemingly freeze.  It is thusly advised that you run your servers one at a time starting with topaz_connect, then topaz_game, then topaz_search until they all say they are ready (the search one is the fastest, it will pretty much be ready as soon as it's run).  However, once topaz_game has done everything it needs to do and has run for a certain amount of time aftwards, it will only use about 250MB by itself, adding about 1.5MB give or take for additional players, and the other 2 servers use very little.  It is recommended, for this reason, that you disable areas you are not going to use on your server.  This can be done by changing the IP address of the zones in zone_settings in your database, or removing the zone from zone_settings.  You can also cluster zones to different machines, and use other Pis or computers to host them.
#### Power
Raspberry Pis require at least a 2.5amp power supply to run at full power, if you are getting a little yellow lightning bolt in the top right, you have hit the limit of your current power supply, and may not be able to take full advantage of your CPU's power, and may lose connectivity to Bluetooth, or USB devices.

Should you hit either of these 2 limitations, it will take considerably longer for the process to finish, my Pi 3b ran for 12 hours and never finished loading all the zones and reducing the RAM usage to normal ranges.
