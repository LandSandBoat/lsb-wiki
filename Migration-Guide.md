# Migrating from older versions of Topaz or Topaz Next
- [Windows 10](Server-setup-and-maintenance-Windows-10#update)
- [Linux](Server-Setup-and-Maintenance-Linux#update)

# Migrating from Darkstar Project

## If you mostly left it alone (or don't care about your custom changes)
1. Git Clone LandSandBoat's repository
    * ❗ Downloading zip is **_highly discouraged_**
2. Compare and integrate changes you made to your configuration files from your Darkstar's `confs\` folder to your fresh LandSandBoat's `settings\default` folder
    * On your fresh LandSandBoat server, **copy** all of the files from the `server\settings\default\` folder into the `server\settings\` folder.
    * Open the copied files (with the default Windows text editor (Notepad) or an external one (like [Notepad++](https://notepad-plus-plus.org/)).
    * Due to structural/formatting changes, you are not able to just copy and paste the .conf files into the `settings\` folder. You must manually compare changes you made to your .conf file and find their twin in the .lua settings files to set!
        * Any .lua file(s) (in `settings\`) that you do not modify can remain in the `server\settings\default\` folder (the .lua files in the `server\settings\default` folder are used if updated ones are not found in the `server\settings\` folder). 
    * ❕ Do _not_ compile or run the server yet
3. Follow steps on the [Database Management page](Database-Management) to use the dbtool to backup and update your SQL database.
    * ⚠️ You will need Python 3, pip, and the dbtool's dependencies `py -3 -m pip install -r requirements.txt`
4. [Compile the server. LandSandBoat exclusively uses CMake](CMake-Build-Guide), which is a different build process from Darkstar Project
5. Try booting it!
    
## If you made many custom changes
1. Hopefully you properly cloned Darkstar Project, have a proper git history, and have been making your changes as git commits
    * ❌ If you don't meet the above requirements, your situation is outside the current scope of this guide
2. Add LandSandBoat as a [git remote](https://git-scm.com/docs/git-remote.html) for your local git repository
    * 💻 In Git bash: `git remote add LSB https://github.com/LandSandBoat/server.git`
3. Fetch/pull LSB into your local repository
    * 💻 In Git bash: `git pull landsandboat base`
    * ❕ This will also pull all changes made to LandSandBoat since the last time you updated
4. Resolve any merge conflicts
5. For your custom changes, you may need to edit them to reflect the project moving from the `dsp` and `tpz` namespaces to the `xi` namespace
    * 🛠️ (Todo: Fill out this section with required changes)
6. Compare and integrate changes you made to your  configuration files from your Darkstar's `confs\` folder to your fresh LandSandBoat's `settings\default` folder
    * On your fresh LandSandBoat server, **copy** all of the files from the `server\settings\default\` folder into the `server\settings\` folder.
    * Open the copied files (with the default Windows text editor (Notepad) or an external one (like [Notepad++](https://notepad-plus-plus.org/))
    * Due to structural/formatting changes, you are not able to just copy and paste the .conf files into the `settings\` folder. You must manually compare changes you made to your .conf file and find their twin in the .lua settings files to set!
        * Any .lua file(s) (in `settings\`) that you do not modify can remain in the `server\settings\default\` folder (the .lua files in the `server\settings\default` folder are used if updated ones are not found in the `server\settings\` folder). 
    * ❕ Do _not_ compile or run the server yet
7. Follow steps on the [Database Management page](Database-Management) to use the dbtool to backup and update your SQL database.
    * ⚠️ You will need Python 3, pip, and the dbtool's dependencies `py -3 -m pip install -r requirements.txt`
8. [Compile the server. LandSandBoat exclusively uses CMake](CMake-Build-Guide), which is a different build process from Darkstar Project
9. Try booting it!
