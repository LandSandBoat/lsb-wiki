<details>
  <summary>Windows 10</summary>
  
  ## To Install
  * Install [Git for Windows](https://gitforwindows.org/), accept defaults, change default text editor if desired.
  * Install [Visual Studio 2019](https://visualstudio.microsoft.com/vs/community/), check Desktop development with C++.
  * Install [MariaDB](https://mariadb.org/), use defaults, set a root password.
  * Install [Python 3](https://www.python.org/downloads/), check to add to PATH.
  * Open a PowerShell window and navigate to your chosen install directory.
  * Download the latest code, install Python requirements, and copy the configuration files:
    ```
    git clone --recursive https://github.com/LandSandBoat/server.git
    py -3 -m pip install -r topaz/tools/requirements.txt
    cp topaz/conf/default/* topaz/conf/
    ```
  * Edit the new `login.conf`, `map.conf`, and `search_server.conf` files in `topaz/conf/` and change `mysql_password` to the password set during MariaDB setup.
  * Back in your PowerShell window, move to `topaz/tools/` and build the database:
    ```
    cd topaz/tools
    py -3 dbtool.py
    ```
  * Follow the on-screen instructions.
  * Open the `topaz` root folder in VS2019.
  * [Build the solution in VS2019.](https://github.com/LandSandBoat/server/wiki/CMake-Build-Guide)

  ## To Update
  * Open a PowerShell window and navigate to your `topaz` directory.
  * Stash any changes you've made and pull the latest code from upstream:
    ```
    git stash
    git pull
    git stash pop
    ```
    ⚠️ Pay attention! If you stashed any changes, there is a chance you will see the following:
    >CONFLICT (content): Merge conflict in _**some file**_

    ⚠️ If this happens, you need to manually edit the conflicting files before continuing.
  * Move to `topaz/tools/` and update the database:
    ```
    cd tools
    py -3 dbtool.py update
    ```
  * Open the `topaz` root folder in VS2019.
  * [Build the solution in VS2019.](https://github.com/LandSandBoat/server/wiki/CMake-Build-Guide)
</details>

<details>
  <summary>Linux</summary>
  
  ## To Install
  * Use your package manager to install the following packages or their equivalent:

    <details>
      <summary>Debian/Ubuntu</summary>

      ```
      sudo apt update
      sudo apt install git python3 python3-pip g++-9 cmake make libluajit-5.1-dev libzmq3-dev libssl-dev zlib1g-dev mariadb-server libmariadb-dev
      ```
    * **Debian 10/Ubuntu 18.04:** See the [Linux Setup Guide](https://github.com/LandSandBoat/server/wiki/Server-Setup-and-Maintenance-%5BLinux%5D#install) for information about upgrading to and building with g++-9.
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

  * Download the latest code, install Python requirements, and copy the configuration files:
    ```
    git clone --recursive https://github.com/LandSandBoat/server.git
    pip3 install -r topaz/tools/requirements.txt
    cp topaz/conf/default/* topaz/conf/
    ```
  * Run the following script to improve database security:
    ```
    sudo mysql_secure_installation
    ```
  * Type the following to create a database user with the login _**topaz**_ and password _**password**_, and an empty database called _**tpzdb**_. Change these to improve security:
    ```
    sudo mysql -u root -p -e "CREATE USER 'topaz'@'localhost' IDENTIFIED BY 'password';CREATE DATABASE tpzdb;USE tpzdb;GRANT ALL PRIVILEGES ON tpzdb.* TO 'topaz'@'localhost';"
    ```
  * Edit the new `login.conf`, `map.conf`, and `search_server.conf` files in `topaz/conf/` and change `mysql_login`, `mysql_password`, and `mysql_database` to the information used above (_**topaz**_, _**password**_, and _**tpzdb**_).
  * In the `topaz` directory, prepare and build the executables:
    ```
    mkdir build
    cd build
    cmake ..
    make -j $(nproc)
    ```
  * Wait for the build to complete, then move to `topaz/tools/` and build the database:
    ```
    cd ../tools
    python3 dbtool.py
    ```
  * Select 'Reset DB' and follow the instructions to "reset" the database.

  ## To Update
  * Open the `topaz` directory in a terminal.
  * Stash any changes you've made and pull the latest code from upstream:
    ```
    git stash
    git pull
    git stash pop
    ```
    ⚠️ Pay attention! If you stashed any changes, there is a chance you will see the following:
    >CONFLICT (content): Merge conflict in _**some file**_

    ⚠️ If this happens, you need to manually edit the conflicting files before continuing.
  * Prepare and build the executables:
    ```
    cd build
    cmake ..
    make -j $(nproc)
    ```
  * Wait for the build to complete, then move to `topaz/tools/` and update the database:
    ```
    cd ../tools
    python3 dbtool.py update
    ```
</details>

**Next Step: [Post-Install Guide](https://github.com/LandSandBoat/server/wiki/Post-Install-Guide)**