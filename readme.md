# Lumirank Screen for ACC
### Original work by `Bregfer`, with some code updates and tweaks by `@fholgado`. Licensed under `cc-nc`.

## Description
This is a combination of a 3D printed case, a Nextion display, an Arduino board, and some code that runs on [SimHub](https://www.simhubdash.com/) that enables you to have a dedicated Lumirank screen for your sim rig. The Lumirank display is used in race cars to inform the driver of current flags on course. This currently only works for Assetto Corsa Competizione, although it could probably be made to work for iRacing and other games that have current flag telemetry data.

![Lumirank screen on Bregfer's NSX rig](https://dl.dropboxusercontent.com/s/1whrf0awdydwq2i/IMG_20210315_221242233.jpg)

## Features
Displays the following flags:
- Yellow flags per sector (1/2/3)
- Full course/double yellow
- Green flag for race starts
- White flag for last lap
- Checkered flag for race finish
- Blue flag for fast approaching cars

## Basic Instructions
- Print the case using your 3D printer
- Assemble the hardware by connecting the Nextion screen to your Arduino
- Upload the `NextionBridge` sketch from SimHub to your Arduino
- Use the Nextion uploader to upload the Nextion TFT code to your Nextion screen
- Copy the Nextion template (`.hmijmap` and `.hmistruct` into your SimHub `NextionTemplates` folder
- Enable a Nextion screen in SimHub, making sure to select the `Lumirank` template and the right `COM` port
- Fire up ACC, and give it a spin!

## 3D files included
- The front of the main box (Lid.stl)
- The rear cover (Rear.stl)
- The buttons for printing first Top, bottom and small buttons.stl (Optional)

[Thingiverse link](https://www.thingiverse.com/thing:4678316) 

## Hardware required:
- Nextion 2.8 screen
- Arduino Pro Micro (not required if you don't use the LEDs - a TTL converter would work instead, but I used Arduino)
- Micro USB cable (Either ends to make you own cable or chop one up, also it needs 4 wires not 2)
- 4pcs - M3 nuts.
- 4pcs - M3x16 countersunk screw
- 1pcs - 4 pin JST connector
- 1pcs - Micro USB cable
- 1pcs - LED array (4 long) - I used https://www.banggood.com/5pcs-CJMCU-354-4-Bit-Colorful-Lantern-Development-Board-RGB-LED-Programmable-p-1318464.html?rmmds=myorder&cur_warehouse=CN but a single LED that you can wire would also work.
- Some wire

## Instructions for build:
- Print the lid and rear parts. remove the support material from the side holes.
- Push m3 nuts into the recesses in the body, glue may be required depending on print but mine did not require any.
- Wire the LED array:
	- + to VCC
	- - to GND
- Din to pin 3 of arduino.
- Place the LED array in the slot for it and route the wire around the indent and up the side.s
- Place the Nextion screen into the lid, with the JST connection at the side opposite the wire hole.
- If you are using a micro USB cable, chop it close to the micro end, strip it, push it through the hole and resolder the wires. If you are making your own end, wire it. Once the wire is in its intended that a cable tie act as a strain relief, I found mine to be slightly too thick for this, your milage may vary.
- Solder 4 wires on to the JST connector and wire them up to Arduino:
```
	Nextion <-> 	Arduino
		5V	-	RAW
		TX	-	RX
		RX	-	TX
		GND	-	GND
```
- Stick the Arduino down in the box somehwere. Hot glue is nice to attach it to the back of the Nextion screen.
- Put the lid on and attach with the m3x20mm screws.
- Optional: Print out the sticker in the PDF file for an extra tenth in your lap times.

Construction complete.

## Instructions for software:

1. Install simhub, you need that.
2. Upload Nextion Micro Bridge sketch to arduino, its found in the simhub directory under 'Nextion Micro Bridge', If you have the LED you need to change the top part of the sketch to include LEDs, of which there are 4, and the data pin should be set to 3. Select the correct arduino type and COM port for the Arduino in the settings then upload. If you are unsure which COM port to use, look at the 'ports' section of windows device manager and see which one comes and goes as you plug and unplug it. If nothing appears, check your wiring to arduino. Nextion wiring does not affect this yet.
3. Upload Nextion template, in the Nextion files provided, double click the .tft file to open the Nextion uploader. This may take several attempts with unplugging and plugging the device in (usually twice) but eventually it should start uploading and complete. If you are having trouble - the screen should be showing some default Nextion stuff while plugged in, if not check wiring. If its lit up but failing to upload, check TX and RX wires are the right way round (they are crossed between Nextion and Arduino). Make sure Simhub isnt open when you upload, the port has to be free, close all other software or restart machine.
4. Set up Nextion within simhub, select the template file from the drop down menu and choose the one provided. It works by temporarily activating a screen when a flag appears, so setup each screen with a Conditional trigger, with the trigger being the flag.

Have fun with it!