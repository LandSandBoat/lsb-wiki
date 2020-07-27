## How to make a dump file with Visual Studio 2019

(Make sure you're running your servers and you identified a crash for which you've been asked to provide a dump file.)

Execute Visual Studio 2019 > Debug > Attach to Process... > select topaz_game.exe in the list > Attach.

Once the crash is reproduced while being monitored by Visual Studio 2019:

Debug > Save Dump As...

Same steps can be made through the Task Manager:

Right click on the taskbar > Task Manager > Processes > right click on topaz_game.exe > Create Dump File.

---

## Auto-restarting while using GDB

Create a file in your topaz root directory called `multirun.gdb` with the following contents:
```gdb
while 1
  set logging off 
  file topaz_game
  run
  set logging on
  list
  bt
  x/5i $pc-6
end
```

Launch the game with `gdb -x multirun.gdb`.

If gdb catches a fatal crash, it will dump the source location (list), the stack trace (bt), and the last few assembly instructions (x/5i $pc-6) into `gdb.txt`. If you can't diagnose what the issue is from that output, staff will be able to help. The information is appended onto gdb.txt, so it can catch multiple crashes if needed.

The loop is pretty tight, you'll have to spam CTRL+C a few times to get back to the gdb interface. You can then quit with `quit`.