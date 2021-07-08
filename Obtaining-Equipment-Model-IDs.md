This is a simple guide on how to obtain equipment model IDs from retail to implement new items for LandSandBoat. There's a lot of words here, but it really is a simple process.

### Required Software

There may be other methods, but to follow this tutorial, you'll need:

* Access to a retail server (trial account works!)
* Windower 4
* [PacketViewer addon](https://github.com/z16/Addons/tree/master/PacketViewer)
* [PacketViewerLogViewer](https://github.com/ZeromusXYZ/PacketViewerLogViewer/releases)

### Find a Guinea Pig

Now you need to find a person displaying the piece of equipment you want to capture. If they have the item equipped but are displaying a different lockstyle, you can't get the model ID from them. You could try asking nicely to see what it looks like in a tell, I suppose?

The process for picking out the right packet is easier if we can isolate the player far away from other players or NPCs. If you can't lure them elsewhere, you've got to work with what you have.

### Load PacketViewer & Setup Logging

Load PacketViewer with `//lua l packetviewer` and Windower should print a confirmation on your screen.

![PacketViewer is loaded](https://i.imgur.com/C0VVkCt.png)

Now we need to enable logging with `//pv l f i`, which instructs it to log incoming packets to files. There will be no immediate onscreen confirmation of this command, but you will eventually start seeing notices printing in your log. You may see a lot of them suddenly in a busy area.

![Packet being logged to file](https://i.imgur.com/O3sHnih.png)

For future reference in other utilization of PacketViewer, you may want to do `//pv l b i` to enable logging of incoming and outgoing packets to file. That creates additional noise here in our current endeavor, as we only need incoming packets.

### Capturing the Packet

When a player character is either first drawn for your client or when they change their visible gear, that information is sent to your client from the server. Any other time their character needs updated while nearby, the server doesn't send any additional information about that player's gear models because it would be unnecessary.

Knowing that, it's obvious we either need to capture the moment they're first introduced to your client or when they swap from another appearance of the target slot to the desired piece. 

With incoming packets being logged to file, orchestrate for either of these to occur. If the player is idle with the desired item displayed, you may need to go the extra mile and zone back into the area and approach them until they are drawn onscreen again. Sometimes simply exiting draw distance range and returning isn't enough to have a fresh packet sent to your client with their visual information.

With your packet captured, now we move to the final task to obtain the appropriate model ID for your item. You can now unload PacketViewer with a simple `//lua u packetviewer` to stop writing new packets to disk and adding information we don't need to the mix.

*Note: If you've used PacketViewer previously, you may want to first cleanup prior data by archiving it elsewhere or deleting it.*

### Examining the Packet with PacketViewerLogViewer

Now navigate to where you've placed PacketViewerLogViewer (PVLV) and load the program `PVLV.exe`. You will be confronted with a screen that looks like this.

![Fresh PVLV](https://i.imgur.com/xIKIlqu.png)

Click on File-> Open and navigate to the `Windower4/addons/PacketViewer/data/logs` folder on your computer. It should look similar to this once inside. We want to open the `incoming.log` file pictured here.

![PacketViewer log directory](https://i.imgur.com/ytdONfm.png)

Depending on how busy the area was when you were capturing packets, you may see a lot of noise here. This is why operating in a quieter area if possible is ideal, but we can get the information either way. Our primary focus here are the `PC Update` entries you should see on the left hand side. Assuming you captured your guinea pig correctly, they will be one of these!

![PC Update packets in list](https://i.imgur.com/hXL3f7J.png)

Once you've selected one of these packets, the top-right portion of PVLV should populate with some information. Regardless of it being a packet displaying model information or not, it should look similar to this example. We need to be sure it lists your guinea pig's name, as there might be other characters in the area generating packets being sent to you during logging.

![PVLV with PC Update packet chosen](https://i.imgur.com/Y7g9zpZ.png)

So now scroll down inside the top-right box and you might see something like this.

![PC Update packet with no model information](https://i.imgur.com/Fx1Q4Vo.png)

If the model information is `None < = 0 (0x0000)` like displayed above, we did not capture the appearance of the player with the selected PC Update packet. Hopefully you have more of them in the list on the left. If not, you'll have to attempt logging the packet again.

However, if the information is like below and it's of the target character, then great job! You've most likely obtained the right model, unless they swapped gear again during logging. This is why running PacketViewer only when required is a good idea to help eliminate additional noise.

![PC Update packet displaying equipment models](https://i.imgur.com/rHV62uH.png)

Assuming everything went correctly, you now have your desired piece of equipment's model ID. Not so bad, right? The _fun_ part of implementing is really the more tedious entry of the item's information into the database, but that's for another article.

