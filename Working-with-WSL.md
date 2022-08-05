# Working with WSL

It's better to clone your repo to somewhere like `/home/`. It is _incredibly_ slow to use `/mnt/c/`.

From WSL, get the IP of your Windows machine:

```sh
ping "$(hostname).local"
```

Result: `172.30.167.123`

In your MariaDB server:

```sh
CREATE USER 'root'@'172.30.167.123' IDENTIFIED BY 'root';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'172.30.167.123' ;
FLUSH PRIVILEGES;
```

From WSL:

```sh
mysql -h 172.30.160.1 -uroot -proot
> USE xidb;
```

In your map.conf:

```sh
mysql_host:      172.30.160.1
mysql_port:      3306
mysql_login:     root
mysql_password:  root
mysql_database:  xidb
```

```sh
cd server
mkdir build
cmake -S . -B build
cmake --build build -j8
```
