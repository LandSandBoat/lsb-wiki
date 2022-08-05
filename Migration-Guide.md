# Migrating from older versions of Topaz or Topaz Next
- [Windows 10](Server-setup-and-maintenance-Windows-10#update)
- [Linux](Server-Setup-and-Maintenance-Linux#update)

# Migrating from Darkstar Project

## If you mostly left it alone (or don't care about your custom changes)
1. Git Clone Topaz Next's repository
    * ❗ Downloading zip is **_highly discouraged_**
2. Copy your configuration files from your Darkstar's `confs` folder to your fresh Topaz's `confs` folder
    * ❕ Do _not_ compile or run the server yet
3. Follow steps on the [Database Management page](Database-Management) to use the dbtool to backup and update your SQL database.
    * ⚠️ You will need Python 3, pip, and the dbtool's dependencies `py -3 -m pip install -r requirements.txt`
4. [Compile the server. Topaz Next exclusively uses CMake](CMake-Build-Guide), which is a different build process from Darkstar Project
5. Try booting it!
    * ❕ You may see strange new notices about unrecognized configuration settings, as we've changed or removed settings which Darkstar Project had. You can:
        1. Copy a new conf file from the `confs/defaults` folder into `confs/` and reapply your desired changes
        2. Compare your conf file against a default conf file in the `confs/default/` to see what changed and make changes as appropriate

## If you made many custom changes
1. Hopefully you properly cloned Darkstar Project, have a proper git history, and have been making your changes as git commits
    * ❌ If you don't meet the above requirements, your situation is outside the current scope of this guide
2. Add Topaz Next as a [git remote](https://git-scm.com/docs/git-remote.html) for your local git repository
    * 💻 In Git bash: `git remote add topaz https://github.com/LandSandBoat/server.git`
3. Fetch/pull Topaz into your local repository
    * 💻 In Git bash: `git pull topaz release`
    * ❕ This will also pull all changes made to Darkstar Project since the last time you updated
4. Resolve any merge conflicts
5. For your custom changes, you may need to edit them to reflect the project moving from the `dsp` and `tpz` namespaces to the `xi` namespace
    * 🛠️ (Todo: Fill out this section with required changes)
6. Copy your configuration files from your Darkstar's `confs` folder to your fresh Topaz's `confs` folder
    * ❕ Do _not_ compile or run the server yet
7. Follow steps on the [Database Management page](Database-Management) to use the dbtool to backup and update your SQL database.
    * ⚠️ You will need Python 3, pip, and the dbtool's dependencies `py -3 -m pip install -r requirements.txt`
8. [Compile the server. Topaz Next exclusively uses CMake](CMake-Build-Guide), which is a different build process from Darkstar Project
9. Try booting it!
    * ❕ You may see strange new notices about unrecognized configuration settings, as we've changed or removed settings which Darkstar Project had. You can:
        1. Copy a new conf file from the `confs/defaults` folder into `confs/` and reapply your desired changes
        2. Compare your conf file against a default conf file in the `confs/default/` to see what changed and make changes are appropriate