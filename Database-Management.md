The database update, backup, and restore tool is called dbtool and is located in the `topaz/tools/` folder. You can execute it using Python3 by typing `py -3 dbtool.py` in a PowerShell window on Windows or `python3 dbtool.py` in a Linux terminal. After opening it, it will create a `config.yaml` file that saves its settings.

# Backup
- Using the default interface, select "3. Backup" and press `y` to create a full database backup in `topaz/sql/backups/`.

**OR**

- Use the command `dbtool.py backup` to create a full database backup in `topaz/sql/backups/`.

  - Use the command `dbtool.py backup lite` to create a partial database backup in `topaz/sql/backups/`. This will contain only the tables listed in `config.yaml`.

# Restore/Import
- Using the default interface, select "4. Restore/Import", press `y` to create a full database backup or anything else to continue without a backup, then enter the number of the desired backup to import. Read the prompt carefully and confirm the import. 

# Update
- Using the default interface, select "1. Update", press `y` to create a full database backup or anything else to continue without a backup, review the changes then press `y` to import all files in `topaz/sql/` except those defined in `config.yaml`. It will then check for any needed migrations, and finally it will check if there was a version update and if your `version.conf` file should be updated
  - If you have a `DB_VER` saved in your `version.conf` file, then dbtool will offer a new option above "1. Update" called "e. Express Update" if any files need to be updated. It will import only the files marked by git as changed since your last time updating with dbtool.

**OR**

- Use the command `dbtool.py update`. This will create a full backup, perform an express update (defined above), perform any needed migrations, and finally update your targeted client version in `version.conf`.
  - The automatic backup and target client update can be disabled in `config.yaml`.
  - Use the command `dbtool.py update full` to ignore the express part of the update and import all files in `topaz/sql/` except those defined in `config.yaml`.

# ⚠Protected Tables⚠
By default, these files will be left untouched during updates using dbtool. This is also the same list of tables used for `dbtool.py backup lite`. You can edit this list using dbtool or editing `config.yaml`.
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