<details>
  <summary>Windows 10</summary>
  
  ## To Install
  * Install [Git for Windows](https://gitforwindows.org/), accept defaults, change default text editor if desired.
  * Install [Visual Studio 2019](https://visualstudio.microsoft.com/vs/community/), check Desktop development with C++.
  * Install [MariaDB](https://mariadb.org/), use defaults, set a root password.
  * Install [Python 3](https://www.python.org/downloads/), check to add to PATH.
  * Open VS2019
  * Clone from URL https://github.com/project-topaz/topaz.git
  * Open in Explorer, **copy** all files in `topaz/conf/default/` into `topaz/conf/`.
  * Edit the new `login.conf`, `map.conf`, and `search_server.conf` files in `topaz/conf/` and change `mysql_password` to the password set during MariaDB setup.
  * Open the tools folder, shift+right-click, open Powershell.
  * Type:
  ```
  py -3 -m pip install -r requirements.txt
  py -3 dbtool.py
  ```
  * Follow the on-screen instructions.
  * Build the solution in VS2019.

  ## To Update
  * Open the topaz folder in Explorer.
  * Shift+right-click, open Powershell.
  * Type:
  ```
  git stash
  git pull
  git stash pop
  cd tools
  py -3 dbtool.py update
  ```
  * Build the solution in VS2019.
</details>

<details>
  <summary>Linux</summary>
  
  ## To Install
  * Use your package manager to install the following packages or their equivalent, dev version if available: 
`mariadb-server libmariadbclient libluajit-5.1 libzmq3 autoconf pkg-config libssl python3 git`
  * Type:
  ```
  sudo mysql_secure_installation
  ```
  * Follow the instructions for setting up the DB.
  * Type (changing 'password' to your password of choice):
  ```
  sudo mysql -u root -p -e "CREATE USER 'topaz'@'localhost' IDENTIFIED BY 'password';CREATE DATABASE tpzdb;USE tpzdb;GRANT ALL PRIVILEGES ON tpzdb.* TO 'topaz'@'localhost';"
  git clone --recursive https://github.com/project-topaz/topaz.git
  cd topaz
  cp conf/default/* conf/
  ```
  * Edit the new `login.conf`, `map.conf`, and `search_server.conf` files in `topaz/conf/` and change `mysql_login` and `mysql_password` to the login/password set during MariaDB setup.
  * In the `topaz` dir, type:
  ```
  sh autogen.sh
  ./configure --enable-debug=gdb
  make
  cd tools
  pip3 install -r requirements.txt
  python3 dbtool.py
  ```
  * Select 'Reset DB' and follow the instructions to "reset" the database.

  ## To Update
  * Open the `topaz` dir in a terminal.
  * Type:
  ```
  git stash
  git pull
  git stash pop
  sh autogen.sh
  ./configure --enable-debug=gdb
  make
  cd tools
  python3 dbtool.py update
  ```
</details>
