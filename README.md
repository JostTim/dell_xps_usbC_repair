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

### Logic schematic

Both the logic schematic pdf file and the cad circuit board file were obtained from the [BadCaps.net](https://www.badcaps.net/) forum, on [this thread](https://www.badcaps.net/forum/troubleshooting-hardware-devices-and-electronics-theory/troubleshooting-laptops-tablets-and-mobile-devices/schematic-requests-only/81147-dell-xps-13-9370-compal-la-e671p-caz60-scheme).

### CAD file
- The .cad file (wich is a GenCad file version 1.4) can be opened with the  ``OpenBoardView`` open source viewer, all credit and thanks to the developpers.  
- The sources for this viewer are available at https://github.com/OpenBoardView/OpenBoardView.  
- A compiled version for windows32 (version 9.95.1) is provided in the current repository's ``./utilities`` fol der.

### Solder Pads reparation
- Using `Wylie Solder Pad Repair Kit`. A video is available [here](https://www.youtube.com/watch?v=MnlAi9IiHt8) showing how to use it. It seems pretty tideous but very reliable in cases that seem to be lost and precious causes. (for ecological repair reasons, cost reasons, or because boards are not manufactured anymore)
 
### InterSil product ISL88738 change Notice

If seems from this datasheet available at [Mouser](https://www.mouser.com/PCN/Intersil_PCN17048_customer_notice.pdf) that the ISL88738 component family had an internal change mid production, as some units showed issues with the threshold for Way Overcurrent Protection, too sensitive to input voltages, and triggering protection under normal operation. (could be the cause of our issue ?)
If the component on my motherboard dates from before this change, that could explain the issue, and why it sometimes auto resolve, as this is pretty a "sensitive" bug, always on the edge of being triggered.

### ISL88738 Replacement Chip 

Available for cheap at [AliExpress](https://fr.aliexpress.com/i/32896388346.html?gatewayAdapt=glo2fra) 


### Replacement LA-E671P motherboard

Available for 200 euros at [Aliexpress](https://fr.aliexpress.com/item/1005006002987787.html?spm=a2g0o.productlist.main.27.749cLtDeLtDeS8&algo_pvid=67b03472-11c3-4d06-ad58-83546293aeb9&algo_exp_id=67b03472-11c3-4d06-ad58-83546293aeb9-13&pdp_npi=4%40dis%21EUR%2182.69%2182.69%21%21%2184.10%2184.10%21%40211b61a417353563282152359ebd7b%2112000035266947213%21sea%21FR%210%21ABX&curPageLogUid=VBW9wCv5wXLK&utparam-url=scene%3Asearch%7Cquery_from%3A)

Another option [here](https://fr.aliexpress.com/item/1005005680576024.html?spm=a2g0o.productlist.main.1.171e3d61l9vWy2&algo_pvid=d267c33f-2e7e-4e5e-ab9f-ef13c1ce7d5d&algo_exp_id=d267c33f-2e7e-4e5e-ab9f-ef13c1ce7d5d-0&pdp_npi=4%40dis%21EUR%21120.11%21112.11%21%21%21122.16%21114.02%21%40211b81a317353411380133012e18e3%2112000033991561507%21sea%21FR%210%21ABX&curPageLogUid=ZrUNW27IwgQO&utparam-url=scene%3Asearch%7Cquery_from%3A)


[Reparation offer on ebay](https://www.ebay.fr/itm/265759479461?itmmeta=01JG5NYF77NXR9BKY8ZZKRNW3G&hash=item3de07fd6a5:g:aPQAAOSwYQFivVhK), using the provider [SLE-France](https://sle-france.com/), for about 250 euros.

### Other similar or related cases

- Reported case of USB-C power circuit faulting on another XPS of similar generation : https://www.dell.com/community/en/conversations/xps/dell-xps-15-9570-usb-c-power-circuit-is-a-bad-design-broke-2x-in-6-years/675e0221d3407a439dfbc25c

- Example case of blowns chip for the power line on the motherboard of a similar generation  XPS laptop. The ``ISL88738`` is the chip that is damaged here : https://www.badcaps.net/forum/troubleshooting-hardware-devices-and-electronics-theory/troubleshooting-laptops-tablets-and-mobile-devices/3534980-dell-xps-9570-blown-isl88738-trace-repair 

- Example of power cycling after damage has been done to the ISL88738 chip : https://boards.rossmanngroup.com/threads/dell-xps-15-9570-la-g341p-power-cycling-after-liquid-damage-and-blown-isl88738.63197/

- Bios related DisplayPort and USB-C issues : https://www.dell.com/community/en/conversations/xps/xps-13-9300-bios-1010-usb-type-c-to-dp-adapters-no-longer-work/647f887ff4ccf8a8de7ebe2f

- USB-C port disconnecting / high CPU usage : https://www.dell.com/community/en/conversations/xps/usb-device-problems-on-left-usb-c-portcontroller-xps13-9300/647f89faf4ccf8a8de9aee4c

- Issues with power and dock usb-C ports : https://forums.tomshardware.com/threads/strange-usb-device-issue-usb-devices-fall-off-dell-win11-laptop-connected-via-dell-dock.3836198/

- Issues with a usb port not working and disabling powershare in BIOS solves it :https://www.reddit.com/r/Dell/comments/5jl1kt/dell_xps_13_kabylake_9360_right_usb_port_not/

- Usb ports not working after a windows update : (https://www.dell.com/community/en/conversations/xps/xps-13-9370-usb-c-ports-not-working-after-windows-10-updates/647f90f2f4ccf8a8de255760)

### Miscelaneous 

- Dell XPS 13 9370 Light error codes : https://www.dell.com/support/manuals/fr-fr/xps-13-9370-laptop/xps-13-9370-servicemanual/system-diagnostic-lights?guid=guid-f7e24b39-9988-47a8-8c7b-4f85ba0cf5dd&lang=en-us

- Dell XPS 13 9370 replacement back plastic cover for the hinge https://fr.aliexpress.com/item/4001287457095.html?gatewayAdapt=glo2fra

- Kapton Tape (for insulation and high thermal resistance / dissipation)