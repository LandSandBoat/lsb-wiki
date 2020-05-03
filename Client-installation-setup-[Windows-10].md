## 1. Install, configure and update Final Fantasy XI Ultimate Collection - Seekers Edition

1. [Official link to download US installation files](http://www.playonline.com/ff11us/download/media/install_win.html) (get all of them). These files include updates until april 2019.

2. Extract the files first by executing the "FFXIFullSetup_US.part1.exe" then proceed to the installation through "FFXISetup.exe" (freshly extracted).

3. Once the whole installation is complete, execute PlayOnline Viewer. If an update is available, click on "Next", then: 
* Select "Update" ; once this is done, click on "OK" then "Next". PlayOnline Viewer should restart automatically.
* Select "For PlayOnline Members!".
* On the next screen, enter id like 1234ABCD or ABCD1234 (4 letters 4 number sit doesn't care about the order) (doesn't matter if they're accurate or not) in the "Member Name" and "PlayOnline ID"  fields.
* Click on "Register" > "Yes" > "OK" > "Exit" and finally "Yes".

---

## 2. Updating (_automatic_ way)

1. In the \PlayOnline\SquareEnix\FINAL FANTASY XI\ROM\0 folder > delete the 0.dat file.

2. Execute PlayOnline Viewer. Click on "Check Files" from the list on the left.

3. Select "FINAL FANTASY XI" in the drop-down menu ("PlayOnline Viewer" is selected by default) then click on "Check Files".

4. PlayOnline Viewer will find errors, click on "File Repair" then "Yes".

5. Once everything is done, click on "OK" then "Exit Viewer" and "Yes".

---

## 3. Configuration

1. Start Menu > PlayOnline > FINAL FANTASY XI Config: configure specific options.

2. Download and install [MSVC 2015 Runtimes](https://www.microsoft.com/en-ca/download/details.aspx?id=48145) (if needed).

3. Right click wherever you want to download the xiloader repository > Git Clone... > URL: https://github.com/zircon-tpl/xiloader.git > OK > then Close when it's done.

4. Execute Visual Studio Community 2019: Open a project or solution (on the right) > select the "xiloader.sln" file from the \xiloader\ folder > Open (click "OK" when asked to "Retarget Projects").

5. Once it's loaded > Build > Build Solution.

6. To confirm that everything was built properly, you should see:

> ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========

in the output console at the bottom and the xiloader executable file should be present in the \xiloader\Debug\ folder.
Put it wherever you want but remember it's path.

---

* Execute xiloader.exe as an administrator (after launching both (atleast) topaz) then select the "Create New Account" option by hitting "2" then:
```
Username: Username
Password: Password (then repeat)
```
* After that, with each launch, select the "Login" option by hitting "1" then:
```
Username: Username
Password: Password
```

/!\ NB /!\

Username (3-15) (as displayed on the loader for now): less than 3 characters and more than 15 characters works.
Password (6-15) (as displayed on the loader for now): less than 6 characters works. More than 15 characters works _when you register BUT note_ that typing the first 15 characters when you're tring to log in will let you in.

---

/!\ **or** /!\

---

## 4. Launching via Windower

1. Download [Windower](http://windower.net/).

2. Execute Windower as an administrator and it will download updates automatically.

3. Click on the pen to edit the "Default Profile" and modify it's options at your will.

4. Open the settings.xml file and set your options as follow (don't forget to save changes):

```
<profile name="Username">
  <args>--server Server.IP.address --user Username --pass Password</args>
  <executable>HDD:\path\to\xiloader.exe</executable>
</profile>
```

5. Execute Windower.exe.

6. Select your profile and click on the arrow (bottom right), it will launch xiloader.

## 4b. Launching via Ashita

1. Download [Ashita] (https://www.ashitaxi.com/)

2. Run Ashita as administrator

3. Click on the Plus icon to make a new configuration, then edit the file line with the file path to your xiloader (can use the ... to browse)

4. in the command line, place your server details as --server yourserverip --hairpin (if externally facing). You can also use --user and -pass to autopopulate  your credentials.

5. Choose window to adjust your resolution if need be.

6. click the paper icon to save, launch with the red arrow. 