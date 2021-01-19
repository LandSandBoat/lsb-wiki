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
    git clone --recursive https://github.com/topaz-next/topaz.git
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
  * [Build the solution in VS2019.](https://github.com/topaz-next/topaz/wiki/CMake-Build-Guide)

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
  * [Build the solution in VS2019.](https://github.com/topaz-next/topaz/wiki/CMake-Build-Guide)
</details>

<details>
  <summary>Linux</summary>
  
  ## To Install
  * Use your package manager to install the following packages or their equivalent:

    **Debian/Ubuntu:**
    ```
    sudo apt install g++-8 make cmake libluajit-5.1-dev libzmq3-dev libssl-dev python3 python3-pip git mariadb-server libmariadb-dev
    ```
    **Arch:**
    ```
    sudo pacman -S gcc make cmake luajit zeromq openssl python3 python-pip git mariadb
    ```
    * Arch users will need to initialize and start the database software if not done already:
        ```
        sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
        sudo systemctl enable mariadb
        sudo systemctl start mariadb
        ```
  * Download the latest code, install Python requirements, and copy the configuration files:
    ```
    git clone --recursive https://github.com/topaz-next/topaz.git
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
