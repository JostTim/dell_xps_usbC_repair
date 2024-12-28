# dell_xps_usbC_repair

## Observations :

My dell laptop (XPS13 9370, i7 16Gb) showed sudden weird behaviour. 
This behaviour form is made of several interlinked symptoms : 
- the usb-c based charger started to elicit slow blinks of charge / not charge on the led and on the computer charging utility reporter, every 2 to 4 seconds or so, 
- these periods of not charging, wich occupied most of the "ON" time of the computer, were correlated with slow, laggy behaviour of the OS, whatever the charge level (even if it is 95%, when it fails to charge or be plugged to the grid in a stable manner, it laggs a bit)
- the laptop integrated keyboard was completely "jammed" during these periods, in the sense that some keypresses are not recognized, or with a delay, and sometimes get repeated a lot of times even with a single keypress, rendering any interaction with the computer impossible
- on top of the other symptoms, the usb C ports (all of them) are not useable for plugging external drives or peripherals, they don't make them appear in the OS nor the BIOS, or if they do appear, it is for a flash of time (usb device get detected, then disapear from os, and reappear, every 2/4 sec or so, and ultimately stops being detected) 
- These symptoms, while left plugged in the usb-c port for a while, sometimes disapear, like if the usb charger and computer finally negotiated a voltage successfully. When the symptoms disapeared, as long as the computer is not turned off, the normal behaviour of the pc is alright (no lags, no issues with keyboard or usb ports) and the power cable can even be disconnected a few tens of seconds and it can then be replugged and renegociate corectly. It's like the problem stop happening in thoses cases. 
- This last observation initially lead me to think the issue could be software ? 
- I tried reinstalling the OS (windows) then installing a different OS (linux mint), and the keyboard press issue and usb drives detection occurs exactly in the same way regardless of the OS, and even occus in the BIOS, so it seems pretty low level.
- I tried several usb C power delivery capable power supplies, with 45+W  (20V 2.25A or more) rated power. The result is the same regardless (Dell charger or not). Also, none of the observed behaviour occured while using these chargers for over a several years before the first occurence of the bug.



## Ressources

All of them have been gathered online, all credit to their authors / providers, and are just centralized here for reference if the issue occurs again.

### ISL88738 Datasheet

The ISL88738 datasheet is quite restrained and lacks proper informations. It seem to be available upon request.
It is a buck / boost converter that is designed to recieve power from the USB-C powere delivery line, or the battery, feed the battery if need be, and feed the power lines of the computer. That is quite a pivotal chip in the powere line design of the motherboard, hence i suppose it may be the source of the bug, that seem to have impacts over a large set of elements (could also be be a faulty power line that collapses, downstream, like a 5V one for keyboard and USB ports, but then i would't understand why it also affects the charging state of the whole computer.)

### CAD file
- The .cad file (wich is a GenCad file version 1.4) can be opened with the  ``OpenBoardView`` open source viewer, all credit and thanks to the developpers.  
- The sources for this viewer are available at https://github.com/OpenBoardView/OpenBoardView.  
- A compiled version for windows32 (version 9.95.1) is provided in the current repository's ``./utilities`` folder.

### Solder Pads reparation
- Using `Wylie Solder Pad Repair Kit`. A video is available [here](https://www.youtube.com/watch?v=MnlAi9IiHt8) showing how to use it. It seems pretty tideous but very reliable in cases that seem to be lost and precious causes. (for ecological repair reasons, cost reasons, or because boards are not manufactured anymore)
 
### InterSil product ISL88738 change Notice

If seems from this datasheet available at [Mouser](https://www.mouser.com/PCN/Intersil_PCN17048_customer_notice.pdf) that the ISL88738 component family had an internal change mid production, as some units showed issues with the threshold for Way Overcurrent Protection, too sensitive to input voltages, and triggering protection under normal operation. (could be the cause of our issue ?)
If the component on my motherboard dates from before this change, that could explain the issue, and why it sometimes auto resolve, as this is pretty a "sensitive" bug, always on the edge of being triggered.

### ISL88738 Replacement Chip 

Available for cheap at [AliExpress](https://fr.aliexpress.com/i/32896388346.html?gatewayAdapt=glo2fra) 


### Other similar or related cases

- Reported case of USB-C power circuit faulting on another XPS of similar generation : https://www.dell.com/community/en/conversations/xps/dell-xps-15-9570-usb-c-power-circuit-is-a-bad-design-broke-2x-in-6-years/675e0221d3407a439dfbc25c

- Example case of blowns chip for the power line on the motherboard of a similar generation  XPS laptop. The ``ISL88738`` is the chip that is damaged here. : https://www.badcaps.net/forum/troubleshooting-hardware-devices-and-electronics-theory/troubleshooting-laptops-tablets-and-mobile-devices/3534980-dell-xps-9570-blown-isl88738-trace-repair 

- 


