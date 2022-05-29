In your MariaDB server:
```
CREATE USER 'root'@'172.30.167.123' IDENTIFIED BY 'root';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'172.30.167.123' ;    
FLUSH PRIVILEGES;
```

From WSL:
```
mysql -h 172.30.160.1 -uroot -proot
> USE xidb;
```

In your map.conf:
```
mysql_host:      172.30.160.1
mysql_port:      3306
mysql_login:     root
mysql_password:  root
mysql_database:  xidb
```