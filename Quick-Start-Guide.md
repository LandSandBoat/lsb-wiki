# Main Supported Platforms

**NOTE:** While it's possible to achieve the steps in this guide using different tools and versions of the software we list, we _cannot recommend enough_ following this guide to the letter and make sure you have everything working before you stray from the well-tested path.

<details>
  <summary>Windows 10</summary>

## To Install

* Install [Git for Windows](https://gitforwindows.org/).
  * The latest version is fine, accept defaults, change default text editor if desired.
* Install [Visual Studio](https://visualstudio.microsoft.com/vs/community/).
  * `2019` or `2022` are fine, check `Desktop development with C++` workload (under Desktop & Mobile).
* Install [MariaDB Server](https://mariadb.org/download/?t=mariadb&p=mariadb&r=10.6.12&os=windows&cpu=x86_64&pkg=msi&m=xtom_ams).
  * Use the latest in the `10.6.x` family of releases, default settings are mostly OK - aside from:
    * **Set a root password**.
    * **Use UTF8 as character set**.
    * **IT IS INCREDIBLY IMPORTANT** that you check the `Use UTF8 as server's character set` checkbox on the `Default instance properties` page during installation. If you don't do this you may face very hard to diagnose crashes.
* Install [Python 3](https://www.python.org/downloads/).
  * The latest version is fine, during installation check the `add python.exe to PATH` checkbox.
* Open a PowerShell window and navigate to your chosen install directory.
* To download the latest code, install Python requirements, and copy the configuration files:

```ps
git clone --recursive https://github.com/LandSandBoat/server.git
py -3 -m pip install -r server/tools/requirements.txt
cp server/settings/default/* server/settings
```

* Edit the file `network.lua` inside `server\settings\` and change "root" to the password set during MariaDB setup
  * Make sure to leave the quotation marks surrounding the password!
* Edit the file `main.lua` inside `server\settings\` with your desired settings for your server.
  * Make sure to leave the quotation marks surrounding that has them around it!
* Back in your PowerShell window, navigate to `server\tools\` and build the database:

```ps
py -3 dbtool.py
```

* Follow the on-screen instructions:

```txt
Please enter the path to your MySQL bin directory or press enter to check PATH.
e.g. C:\Program Files\MariaDB 10.6\bin\
```

```txt
Database xidb does not exist.
Would you like to create new database: xidb? [y/N]
```

* You will eventually get to the main `dbtool` menu.

```txt
o------------------------------------------o
|  LandSandBoat Database Management Tool   |
|            Connected to xidb             |
|                  #e222b                  |
o------------------------------------------o
| 1. Update DB                             |
| 2. Check migrations                      |
| 3. Backup                                |
| 4. Restore/Import                        |
| r. Reset DB                              |
| t. Maintenance Tasks                     |
| s. Settings                              |
| q. Quit                                  |
o------------------------------------------o
```

* You can exit out of `dbtool` now with `q`.
* Open the `server` root folder in `Visual Studio 2019/2022`.
  * `Open a local folder` on the splash screen.
* The build will start configuring itself for your system.
  * This stage is done when the `CMake` window at the bottom of the window says `1> CMake generation finished.`.
* Ensure the dropdown near the top of the window says `x64-Debug`.
* In the top toolbar, select `Build > Build All`.
  * This may take a little while!
* You should eventually see `Build All succeeded.`.
  * Congratulations, you've built the server! You can now go onto [Next Steps](#next-steps).

## To Update

* **Take down all of your server processes!**
* Open a PowerShell window and navigate to your `server` directory.
* Stash any changes you've made and pull the latest code from upstream:

```ps
git stash
git pull
git submodule update --init --recursive --progress
git stash pop
```

⚠️ Pay attention! If you stashed any changes, there is a chance you will see the following:

>CONFLICT (content): Merge conflict in _**some file**_

⚠️ If this happens, you need to manually edit the conflicting files before continuing.

* Navigate to `server\tools\` and update the database:

```ps
py -3 dbtool.py update
```

* Open the `server` root folder in VS2019/2022.
  * CMake _may_ reconfigure, wait for it to complete like before.
* In the top toolbar, select `Build > Build All`.
  * This may take a little while if you have a weaker machine.
* You should eventually see `Build All succeeded.`.

</details>

<details>
  <summary>Linux (Debian/Ubuntu 22.04)</summary>

## To Install

```txt
NOTE: We try to keep up to date with whatever the latest LTS release of Ubuntu is (Ubuntu 22.04). We run all of our CI builds on this release. We can't guarantee that older LTS versions will work. When in doubt, update!
```

* Run these steps to use Mariadb's community provided .deb packages through apt:
  * https://mariadb.com/docs/connect/programming-languages/c/install/#connector-c-install-repo-configure-cs
* Use your package manager to install the following packages or their equivalents:

```sh
sudo apt update
sudo apt install git python3 python3-pip g++-10 cmake make libluajit-5.1-dev libzmq3-dev libssl-dev zlib1g-dev mariadb-server libmariadb-dev binutils-dev
```

* Download the latest code, install Python requirements, and copy the configuration files:

```sh
git clone --recursive https://github.com/LandSandBoat/server.git
pip3 install -r server/tools/requirements.txt
cp server/settings/default/* server/settings
```

* Run the following script to improve database security:

```sh
sudo mysql_secure_installation
```

* Type the following to create a database user with the login <ins>_**xi**_</ins> and password <ins>_**password**_</ins>, and an empty database called <ins>_**xidb**_</ins>. NOTE: You _SHOULD_ change **ALL THREE OF THESE** to improve security:

```sh
sudo mysql -u root -p -e "CREATE USER 'xi'@'localhost' IDENTIFIED BY 'password';CREATE DATABASE xidb;USE xidb;GRANT ALL PRIVILEGES ON xidb.* TO 'xi'@'localhost';"
```

* Edit the file `network.lua` inside `server/settings/` and change the `SQL_LOGIN`, `SQL_PASSWORD`, and `SQL_DATABASE` to the login, password, and database you used in the above command (default xi, password, xidb).
  * Make sure to include the quotation marks!
* Edit the file `main.lua` inside `server/settings` with your desired settings for your server.
  * Make sure to leave the quotation marks surrounding that has them around it!
* In the `server` directory, prepare and build the executables:

```sh
mkdir build
cd build
cmake ..
make -j $(nproc)
```

* Wait for the build to complete, then move to `server/tools/` and build the database:

```sh
cd ../tools
python3 dbtool.py
```

* Select 'Reset DB' and follow the instructions to "reset" the database.

* Congratulations, you've built and set up the server! You can now go onto [Next Steps](#next-steps).

## To Update

* **Take down all of your server processes!**
* Open the `server` directory in a terminal.
* Stash any changes you've made and pull the latest code from upstream:

```sh
git stash
git pull
git submodule update --init --recursive --progress
git stash pop
```

⚠️ Pay attention! If you stashed any changes, there is a chance you will see the following:

>CONFLICT (content): Merge conflict in _**some file**_

⚠️ If this happens, you need to manually edit the conflicting files before continuing.

* Prepare and build the executables:

```sh
cd build
cmake ..
make -j $(nproc)
```

* Wait for the build to complete, then move to `server/tools/` and update the database:

```sh
cd ../tools
python3 dbtool.py update
```

</details>

# Experimental Platforms

**NOTE:** These platforms should work, but are not actively maintained or used by the development team. The development team (especially in the case of OSX) might not have the hardware or expertise to be able to help you debug problems on these platforms. Use at your own risk. Good luck!

<details>
  <summary>OSX</summary>

## To Install

* Get dependencies from brew:

```sh
brew install git pkg-config autoconf make cmake gcc openssl mariadb zeromq zmqpp
```

* The version of LuaJIT that you can get through brew is old. You can build and install LuaJIT for your system with:

```
git clone https://github.com/LuaJIT/LuaJIT.git
cd LuaJIT
sudo make install MACOSX_DEPLOYMENT_TARGET=$(sw_vers -productVersion) -j $(sysctl -n hw.physicalcpu)
sudo ln -sf luajit-2.1.0-beta3 /usr/local/bin/luajit
```

* Download and build the server binaries:

```
git clone --recursive https://github.com/LandSandBoat/server.git
mkdir build
cd build
cmake ..
make -j $(sysctl -n hw.physicalcpu)
```

From here, the instructions are the same as the Linux builds. Good luck!

NOTE: You may have problems with missing symbols from LuaJIT. This happens if the build system picks up LuaJIT's headers instead of our internal (and expected) ones. We discovered this in [this discussion](https://github.com/LandSandBoat/server/discussions/1015).

In your CMake configuration, you should see this:
```
-- LuaJIT_FOUND: TRUE
-- LuaJIT_LIBRARY: /usr/local/lib/libluajit-5.1.dylib
-- LuaJIT_INCLUDE_DIR: /Users/runner/work/server/server/ext/lua/include
```

If the `LuaJIT_INCLUDE_DIR` is pointing somewhere other than `<SERVER_ROOT>/server/server/ext/lua/include`, you can change it during CMake configuration by using:
```
cmake .. -DLuaJIT_INCLUDE_DIR=<SERVER_ROOT>/server/ext/lua/include
```

</details>

<details>
  <summary>Linux (through WSL)</summary>

All of the instructions for Linux should be valid for WSL. There are additional points covered in the [Working with WSL](Working-with-WSL) article.

</details>

<details>
  <summary>Linux (Arch)</summary>

Some users have had success building and running on Arch. We can't and won't support Arch as main platform. Good luck!

```sh
echo "Y" | pacman -Syu
echo "Y" | pacman -S sudo
sudo echo "Y" | pacman -S git python3 python-pip gcc cmake make luajit zeromq openssl zlib mariadb binutils
sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
sudo systemctl enable mariadb
sudo systemctl start mariadb
# CMake build as normal
```

</details>

<details>
  <summary>Linux (Raspberry Pi)</summary>

Build instructions should be the same or similar as a regular Linux build. The build process may take a long time, but running the game doesn't take much computing power.

#### Power

Raspberry Pis require at least a 2.5amp power supply to run at full power. If you are getting a little yellow lightning bolt in the top right of your display you have hit the limit of your current power supply. If this happens you may not be able to take full advantage of your CPU's power and may lose connectivity to Bluetooth or USB devices.

Should you hit either of these 2 limitations it will take considerably longer for the build process to finish, if it finishes at all!

#### LuaJIT

Depending on your distro, the LuaJIT that comes through the package manager may not have required fixes for ARM platforms included with it. It's recommended you follow the steps in the OSX build guide to build and use the latest LuaJIT.

#### RAM

Each server process startup can be quite resource intensive for both CPU and RAM. Older Raspberry Pis don't have much RAM, so you may need to start up each of the server processes one-by-one to ensure that they start and run correctly.

</details>
  
<details>
  <summary>Linux (Gentoo OpenRC)</summary>
  
Ensure your system is up to date:
```sh
sudo emerge --sync && emerge -avuDU @world
```
Emerge the following packages and their dependencies: 
```sh
sudo emerge -a dev-db/mariadb dev-lang/luajit dev-vcs/git net-libs/zeromq
```
Clone the repo in your folder of choice, then copy the settings files:
```sh
cd ~/ && mkdir git && cd ~/git 
git clone --recursive https://github.com/LandSandBoat/server.git
cp server/settings/default/* server/settings
```
MariaDB will need to be configured and the database initialized before the service can be started. If you have issues, or are using Systemd instead of OpenRC, refer to the [Gentoo Wiki](https://wiki.gentoo.org/wiki/MariaDB).
```sh
sudo emerge --config dev-db/mariadb
sudo rc-update add mysql default
sudo rc-service mysql start
```
In order to use dbtool for managing your database, additional packages are required, one of which is not in the main Gentoo repository. This is a problem on Gentoo as installing with pip instead of portage can break your system. Thankfully, with an overlay we can get what we need (ensure you have already installed and configured [eselect-repository](https://wiki.gentoo.org/wiki/Eselect/Repository)):
```sh
sudo eselect repository add claytabase git https://github.com/claybie/claytabase.git
sudo emaint sync -r claytabase
```
Now we can emerge all the necessary packages for dbtool:
```sh
sudo emerge -a dev-python/black dev-python/colorama dev-python/GitPython dev-python/mariadb dev-python/pylint dev-python/pyyaml dev-python/pyzmq dev-python/regex
```
Additionally, you will also need to emerge the below packages if you wish to use [pydarkstar](https://github.com/AdamGagorik/pydarkstar) as an automated auction house:
```sh
sudo emerge -a dev-python/beautifulsoup4 dev-python/sqlalchemy
```
The process for securing the MariaDB installation, creating the SQL database, building the project with make, populating the database using dbtool and performing future updates is the same as on Ubuntu. It can be referenced above from the *Linux (Debian/Ubuntu 22.04)* section.
</details>

<details>
  <summary>Docker</summary>

The core team of LSB does not use Docker in their workflows, and as such can't properly maintain a Docker setup as a first-class citizen. There is an unofficial Docker guide [here](Docker).

</details>

## Next Steps

* The most basic way to start your server is to launch the newly-built `xi_*` executables:
  * `xi_connect.exe`
  * `xi_map.exe`
  * `xi_search.exe`
  * `xi_world.exe`
* Once running, it's a good idea to connect to your server as soon as possible and make sure everything is running as expected.
  * [Client Setup Guide (Windows)](Client-Setup-Windows)
* Once you've confirmed everything is working and you can connect to your server, you can start exploring the [Post-Install Guide](Post-Install-Guide) and [Development Landing Page](Development)!
