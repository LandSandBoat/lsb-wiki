== Executing a MySQL Query ==
Linux and Windows users with MySQL in their PATH can execute a query from the terminal using the following format:
```
mysql -u xi -ppassword xidb -e "QUERY"
```
Where <b>xi</b>, <b>password</b>, <b>xidb</b>, and <b>QUERY</b> are changed to your needs. Windows users can also use the query tab in HeidiSQL (default keybind is ctrl+t).

== Making a Game Master Character ==
After creating your first character you'll want to make it a GM by executing the following MySQL query, replacing <code>Name</code> with your character name:
```
UPDATE chars SET gmlevel = 4 WHERE charname = "Name";
```
Available commands are [https://github.com/LandSandBoat/server/tree/release/scripts/commands found in the scripts/commands/ folder], and a description of each command can be found at the top of the script. Commands can be used in-game using the script name with a preceding <code>!</code>, and removing <code>.lua</code>. For example, <code>promote.lua</code> is ran in game using <code>!promote</code>. This is the command you would use to make additional GMs.

== Changing Game Settings ==
Various details about the game can be changed via editing the settings files. Some settings are located in <code>server/conf/map.conf</code> and require a server reboot to apply. Other settings are found in <code>server/scripts/globals/settings.lua</code> and only require a GM command to reload, <code>!reloadglobal settings</code> (although some settings still require a reboot for full effect). Other files in the <code>server/scripts/globals/</code> folder can be changed in the same way.

== Changing the Server IP Address ==
To make the server accessible over a network, the zoneip must be changed in the zone_settings table. You can do this with a simple MySQL query.
```
UPDATE zone_settings SET zoneip = 'IP';
```
Replace <code>IP</code> with the desired IP. To access the game only on the same machine, this should be <code>127.0.0.1</code>. If you're accessing the server from another machine on the network, it should be the local IP address of the host, e.g. <code>192.168.0.11</code>. If you want to access it over the internet, it needs to be your public IP which can be gathered from various websites such as https://www.whatismyip.com/.

;Note
:<code>zone_settings</code> is not a protected table, so this change can be overwritten during an update. It is recommended to save this query in a <code>.sql</code> file in <code>server/sql/backups/</code> then import it after an update. See [https://github.com/LandSandBoat/server/wiki/Database-Management#making-persistent-changes Database Management].

=== Port Forwarding ===
Make sure you have the following ports forwarded by your router and open in any firewall software if accessing the server over a network:
```
TCP ports: 54230, 54231, 54001, 54002
UDP port: 54230
```

== Database Management ==
By default, dbtool will backup your whole database into <code>server/sql/backups/</code> whenever it performs an update. You can turn this off and do manual backups either with the TUI, or by running <code>python3 dbtool.py backup</code> (Windows: <code>py -3 dbtool.py backup</code>). You can create a backup of only sensitive player data by using <code>python3 dbtool.py backup lite</code> (Windows: <code>py -3 dbtool.py backup lite</code>). The tables it backs up with the <code>lite</code> argument are defined in <code>server/tools/config.yaml</code> (created automatically by dbtool the first time you run it). The backups can be imported using the <b>Restore/Import</b> command in dbtool.

== See Also ==
[https://github.com/LandSandBoat/server/wiki/Miscellaneous-(Server) Common Issues and Tweaks]

[https://github.com/LandSandBoat/server/wiki/Useful-SQL-queries Useful SQL Queries]

[https://github.com/LandSandBoat/server/wiki/Database-Management Database Management]

[https://github.com/LandSandBoat/server/wiki/Debugging Debugging]