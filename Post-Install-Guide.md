# Post-Install Guide

## Changing Game Settings

Various details about the game can be changed via editing the settings files. Settings are located in `settings/` and require a server reboot to apply. If you edit the settings files in `settings/default` nothing will happen. These are used as default values for the settings if you don't copy any files from `settings/default` to `settings/`.

## Executing a MySQL Query ==

Linux and Windows users with MySQL in their PATH can execute a query from the terminal using the following format:

```sh
mysql -u xi -ppassword xidb -e "QUERY"
```

Where **xi**, **password**, **xidb**, and **QUERY** are changed to your needs. Windows users can also use the query tab in HeidiSQL (default keybind is ctrl+t).

## Making a Game Master Character

After creating your first character you'll want to make it a GM by typing `gm TheirName` into your `xi_map` exe's console. You can also do this by executing the following MySQL query, replacing `Name` with your character name (this will require your character to zone to take effect):

```sql
UPDATE chars SET gmlevel = 4 WHERE charname = "Name";
```

Available commands are found in the [scripts/commands/](https://github.com/LandSandBoat/server/tree/base/scripts/commands) folder, and a description of each command can be found at the top of the script. Commands can be used in-game using the script name with a preceding `!`, and removing `.lua`. For example, `promote.lua` is ran in game using `!promote`. This is the command you would use to make additional GMs.

## Changing the Server IP Address

To make the server accessible over a network, the zoneip must be changed in the zone_settings table. You can do this with a simple MySQL query.

```sql
UPDATE zone_settings SET zoneip = 'IP';
```

Replace `IP` with the desired IP. To access the game only on the same machine, this should be `127.0.0.1`. If you're accessing the server from another machine on the network, it should be the local IP address of the host, e.g. `192.168.0.11`. If you want to access it over the internet, it needs to be your public IP which can be gathered from various websites such as <https://www.whatismyip.com/>.

### Note

`zone_settings` is not a protected table, so this change can be overwritten during an update. It is recommended to save this query in a `.sql` file in `server/sql/backups/` then import it after an update. See [Database-Management#making-persistent-changes Database Management].

## Port Forwarding

Make sure you have the following ports forwarded by your router and open in any firewall software if accessing the server over a network:

```txt
TCP ports: 54230, 54231, 54001, 54002
UDP port: 54230
```

## Database Management

By default, dbtool will backup your whole database into `server/sql/backups/` whenever it performs an update. You can turn this off and do manual backups either with the TUI, or by running `python3 dbtool.py backup` (Windows: `py -3 dbtool.py backup`). You can create a backup of only sensitive player data by using `python3 dbtool.py backup lite` (Windows: `py -3 dbtool.py backup lite`). The tables it backs up with the `lite` argument are defined in `server/tools/config.yaml` (created automatically by dbtool the first time you run it). The backups can be imported using the **Restore/Import** command in dbtool.

## See Also ==

[Server Administration](Server-Administration.md)

[Common Tasks](Miscellaneous-Server.md)

[Useful SQL Queries](Useful-SQL-queries.md)

[Database Management](Database-Management.md)

[Development](Development.md)
