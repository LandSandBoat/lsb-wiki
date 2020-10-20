Execute `topaz\tools\dbtool.py` inside a command prompt or bash shell.

_Backup_:

Select "3. Backup" > Enter > "Would you like to backup your database? [y/N]" > y > Enter > Done.

_Restore/Import_:

Select "4. Restore/Import" > Enter > "Would you like to backup your database? [y/N]" > y > Enter > "Choose a number to import, or type "delete #" to delete a file." > select desired backup > Enter > "If this is a full backup created by this tool, it is recommended to manually change the DB_VER in ..\conf\version.conf to the hash sequence in the filename, between the database name and the timestamp, so that express update functions properly. Import _desired-backup.sql_? [y/N]" > y > Enter > Done.

⚠️ 

```
  - accounts.sql
  - accounts_banned.sql
  - auction_house.sql
  - char_blacklist.sql
  - char_effects.sql
  - char_equip.sql
  - char_exp.sql
  - char_inventory.sql
  - char_jobs.sql
  - char_look.sql
  - char_merit.sql
  - char_pet.sql
  - char_points.sql
  - char_profile.sql
  - char_skills.sql
  - char_spells.sql
  - char_stats.sql
  - char_storage.sql
  - char_style.sql
  - char_unlocks.sql
  - char_vars.sql
  - chars.sql
  - conquest_system.sql
  - delivery_box.sql
  - linkshells.sql
  - server_variables.sql
```
These files will be left untouched by default during updates using dbtool. You can manually edit this list using dbtool or editing `topaz\tools\config.yaml`. You can also create a backup of _only_ these tables by opening a PowerShell window in the `topaz\tools\` folder and typing:
```
py -3 dbtool.py backup lite
```