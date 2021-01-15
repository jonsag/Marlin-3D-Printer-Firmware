## Firmware tinkering on Marlin-2.0.7.2 for Geeetech I3 Pro B

Further down in this document are instructions on how to trim, set up and install firmware on your printer.  

Please scroll through whole document so you don't miss anything. :-)  

Instructions below are run on a Linux system.  

Important note - MUST READ
==========
There is line you HAVE to change in configuraton.h before compiling this.  

Uncomment line 1454 to disable my skew correction values.  

	#define XY_SKEW_FACTOR 0.0
	
Comment these out again after you've made the test print and measurements. Read more below.  

(It's not really a disaster if you forget this, but you will get a more skewed print probably.)  


Other changes for different setups
==========
Below are changes you have to do, if you have a different setup than I have.  

IF you DON'T have a BLTouch or clone
----------
Comment out line 907  

	//#define BLTOUCH
	
IF you DON'T have T8 lead screws
----------
Comment out line 744  

	//#define PRO_B_WITH_LEADSCREW
	
IF you have the STOCK LCD screen
---------
Comment out line 2000  

	//#define REPRAP_DISCOUNT_FULL_GRAPHIC_SMART_CONTROLLER
	
and uncomment line 1850  

	#define REPRAP_DISCOUNT_SMART_CONTROLLER
	
If you have a BLTouch or clone, not mounted in the same way I have
----------
Check your probe offsets on line 997  

	#define NOZZLE_TO_PROBE_OFFSET { xx, yy, -zz }
	
Check offsets on lines 1002-  

	#define PROBING_MARGIN_LEFT xx
	#define PROBING_MARGIN_RIGHT xx
	#define PROBING_MARGIN_FRONT yy
	#define PROBING_MARGIN_BACK yy

Check values on line 1386 for the "Level Corners" option  

	  #define LEVEL_CORNERS_INSET_LFRB { xx, yy, xx, yy } // (mm) Left, Front, Right, Back insets
	  
	  
Changes from original firmware release
==========
These are my changes from the source firmware.  
Some things will perhaps have to be adapted to fit your printer setup.  


Makefile
----------
Line 62  

	HARDWARE_MOTHERBOARD ?= 1315
  
>Perhaps not really necessary, but this setting reflects the hardware.


configuration_adv.h
----------
Line 1131  

	#define LCD_SET_PROGRESS_MANUALLY
	
>Enables OctoPrint to update the progress bar on the LCD display. You must also install the plugin M73 Progress, <https://plugins.octoprint.org/plugins/m73progress>, for this to work. If you don't run OctoPrint, this setting will not matter.

 1141  
 
 	#define SHOW_REMAINING_TIME       // Display estimated time to completion
 	
 >Sets M73 command to display time remaining
 
 1144-  
 
	    #define USE_M73_REMAINING_TIME  // Use remaining time from M73 command instead of estimation
	    #define ROTATE_PROGRESS_DISPLAY // Display (P)rogress, (E)lapsed, and (R)emaining time
	    
>Smarter use of M73. Rotates views on LCD display.


configuration.h
----------
Line 73  

	#define STRING_CONFIG_H_AUTHOR "jonsag" // Who made the changes.

> My little mark.
	
130  

	  #define MOTHERBOARD BOARD_GT2560_REV_A_PLUS

>This is essential. Points directly to our hardware setup.
	
134  

	#define CUSTOM_MACHINE_NAME "Geeetech i3 Pro B"

>Puts some text on the display at startup.

426  

	#define TEMP_SENSOR_BED 1
	
>Defines that we have a heated bed, and what type of thermistor.

476  

	#define BED_MAXTEMP      125

>Sets maximum temperature for the heated bed.

498-  

	    #define DEFAULT_Kp_LIST {  22.39,  22.39 }
	    #define DEFAULT_Ki_LIST {   1.91,   1.91 }
	    #define DEFAULT_Kd_LIST { 65.58, 65.58 }

>These are not really used, since we only have one hotend.

502-  

	    #define DEFAULT_Kp  23.12
	    #define DEFAULT_Ki   1.72
	    #define DEFAULT_Kd 77.65

>These are the PID constants that will be used. However I recommend you do a PID tuning as later described.

596  

	//#define THERMAL_PROTECTION_CHAMBER // Enable thermal protection for the heated chamber
	
>If you have a heated and monitored chamber you should uncomment this.

681-  

	#define X_DRIVER_TYPE  A4988
	#define Y_DRIVER_TYPE  A4988
	#define Z_DRIVER_TYPE  A4988

>Not necessary to uncomment, but this now reflects the stock Geeetech drivers.

689  

	#define E0_DRIVER_TYPE A4988

>See above.	

744-  

	#define PRO_B_WITH_LEADSCREW
	#if ENABLED(PRO_B_WITH_LEADSCREW)       // T8 leadscrew version
	  #define DEFAULT_AXIS_STEPS_PER_UNIT   { 81.5, 81.5, 400.69, 108 }
	#else                                   // M8 threaded rod version
	  #define DEFAULT_AXIS_STEPS_PER_UNIT   { 78.74, 78.74, 2560, 105 }
	#endif

> Z steps for T8 lead screws. The added lines are just for conveniance.
	
756  

	#define DEFAULT_MAX_FEEDRATE          { 400, 400, 2, 45 }

>Recommended values. Could be tweaked.

769  

	#define DEFAULT_MAX_ACCELERATION      { 5000, 5000, 50, 5000 }

>See above.

784-  

	#define DEFAULT_ACCELERATION          1000    // X, Y, Z and E acceleration for printing moves
	#define DEFAULT_RETRACT_ACCELERATION  2000    // E acceleration for retracts
	#define DEFAULT_TRAVEL_ACCELERATION   1000    // X, Y, Z acceleration for travel (non printing) moves

>See above.

798  

	 #define DEFAULT_XJERK                 20.0
	 #define DEFAULT_YJERK                 20.0
	 #define DEFAULT_ZJERK                 0.4
  
  >If you enable CLASSIC_JERK on line 796, these are recommended values.  Could be tweaked, but not used now.
  
833  

	#define S_CURVE_ACCELERATION
	
>Better acceleration curve.
	
907-  

	#define BLTOUCH
	#if ENABLED(BLTOUCH)
	  #define BLTOUCH_DELAY 375   // (ms) Enable and increase if 	needed
	#endif

>Essential for BLTouch, and it's clones. Also sets delay.

997  

	#define NOZZLE_TO_PROBE_OFFSET { 20, 2, -0.9}
>The BLTouch's offset from the nozzle. Change these to match your setup.

1002-  

	#define PROBING_MARGIN_LEFT 60
	#define PROBING_MARGIN_RIGHT 0
	#define PROBING_MARGIN_FRONT 0
	#define PROBING_MARGIN_BACK 0

>With these settings I avoid interfering with the clips holding down the glass plate.

1054  

	#define Z_MIN_PROBE_REPEATABILITY_TEST
	
>Enables testing of the repeatability of the level probe.

1101  

	#define INVERT_X_DIR true

>Necessary for our hardware.

1108  

	#define INVERT_E0_DIR true

>See above.
	
1137-  

	#define X_BED_SIZE 186
	#define Y_BED_SIZE 167

>We could adjust this, but now I avoid interferring with the glass bed clamps.
	
1141-  

	#define X_MIN_POS 10
	#define Y_MIN_POS -10

>See above.

1144-  

	#define X_MAX_POS (X_MIN_POS + X_BED_SIZE)
	#define Y_MAX_POS (-Y_MIN_POS + Y_BED_SIZE))
	#define Z_MAX_POS 185

>This is the conclusion of the above settings.
	
1248  

	#define AUTO_BED_LEVELING_LINEAR
	
>You could also uncomment line 1249 instead, or one of the other measurement types. This makes most sense to me.
	
1257  

	#define RESTORE_LEVELING_AFTER_G28
	
>Keeps the leveling data after a G28 home command.

1296  

	#define GRID_MAX_POINTS_X 3
	
>The number of probes in both directions. The value squared is the total number of probes.

1306  

	#define EXTRAPOLATE_BEYOND_GRID

>If you went with bilinear probong above, this is a good setting.
 
1326  

	  #define MESH_EDIT_GFX_OVERLAY   // Display a graphics overlay while editing the mesh

>For unified bed leveling this is a nice feature.

1356  

	#define LCD_BED_LEVELING

>Adds an extra option on how to level the bed.
	
1365  

	#define LEVEL_BED_CORNERS

>A nice feature for do some basic manual leveling.
 
1368  

	  #define LEVEL_CORNERS_INSET_LFRB { 35, 10, 15, 20 } // (mm) Left, Front, Right, Back insets

>Keeps the hotend away from the clamps.

1371  

	  #define LEVEL_CENTER_TOO              // Move to the center after the last corner

>Stop at center when doing the corners.
 
1400  

	#define Z_SAFE_HOMING

>Don't let the probe get outside the bed.
	
1444  

	#define SKEW_CORRECTION

>Enabling this lets your firmware make correctionsto your printer setup. If your axes are not completely perpendicular to each other, which they seldom are, these will be corrected. Read below on how to do this.

1448  

	  #define XY_DIAG_AC 143.55 //142.90 // should be 143.754808615 //282.8427124746
	  #define XY_DIAG_BD 143.95 //143.10 //282.8427124746
	  #define XY_SIDE_AD 101.65
  
>These are MY values AFTER I've done the test print and measuring. You will have enter YOUR values.

1454  

	  //#define XY_SKEW_FACTOR 0.0
	  
>Comment this AFTER you've done the test print and measurements.
 
1468  

	  #define SKEW_CORRECTION_GCODE

>Extra feature for skew correction.
 
1486-  

	#define EEPROM_SETTINGS     // Persistent storage with M500 and M501

>Enables storing of settings with G-code.
	
1518  

	#define PREHEAT_1_TEMP_HOTEND 200
	#define PREHEAT_1_TEMP_BED     65

>Enter whatever values are handy for you.
	
1522  

	#define PREHEAT_2_LABEL       "PETG"
	#define PREHEAT_2_TEMP_HOTEND 235
	#define PREHEAT_2_TEMP_BED    85

>See above.

1739  

	#define SDSUPPORT

>We do have an SD card reader.

1756  

	#define SD_CHECK_AND_RETRY

>This setting makes sense.

1819  

	#define INDIVIDUAL_AXIS_HOMING_MENU

>Handy option to have.
	
1827  

	#define SPEAKER

>Our speaker is capable of putting out some different sounds.

1836-  

	#define LCD_FEEDBACK_FREQUENCY_DURATION_MS 4
	#define LCD_FEEDBACK_FREQUENCY_HZ 5000

>I think button press beeps are nice.

2000  

	#define REPRAP_DISCOUNT_SMART_CONTROLLER

>I have upgraded my printer with this full graphic LCD. If you still have the stock control panel, enable line 1850 instead.
	

Other possible changes in configuration.h
==========


Extra probing
----------
1025  

	#define MULTIPLE_PROBING 3
	  

Compiling and uploading on Arduino IDE
==========
Download and install Arduino IDE 1.8.x from https://www.arduino.cc/en/software  

Open Arduino IDE and open /path/to/Marlin.ini  

Select board:  
Tools -> Board: ... -> Arduino AVR Boards -> Arduino 2560 or Mega 2560  

Select processor:  
Tools -> Processor: ... -> ATmega2560 (Mega 2560)  
 
 Set port:  
Tools -> /dev/ttyUSB0 or whatever...  

Select programmer:  
Tools -> Programmer: ... -> AVRIPS mkII  

Compile and upload!  


Permissions
==========
Check your permissions. You need to belong to the groups tty and dialout to be able to write to the tty/USB.  

Run  
>$ groups | grep ' tty ' && echo -e "\nGreat! \nYou are a member of 'tty'" || echo -e "\nError: \nYou are not a member of the group 'tty'. \n\nCorrect with 'sudo usermod -a -G tty $USER'"

and  
>$ groups | grep ' dialout ' && echo -e "\nGreat! \nYou are a member of 'dialout'" || echo -e "\nError: \nYou are not a member of the group 'dialout'. \n\nCorrect with 'sudo usermod -a -G dialout $USER'"

to check.  

If you had to add yourself to any group, you must reboot to join the groups.  

>$ sudo reboot


Working with binary files
==========
Instead of directly uploading the compiled code with Arduino IDE you can save the compiled code for later upload.  


Export firmware to binary
----------
 Start Arduino IDE and select file and board as above.  

Click 'Sketch -> Export compiled binary'  

The IDE now compiles the firmware to a binary file in the same location as your Marlin.ini.  
It will be called Marlin.ino.mega.hex  

Move the file, and rename it to something sensible.  


avrdude
----------
Install avrdude if not installed.  
>$ sudo apt install avrdude

avrdude is already a part of the Arduino IDE, but this makes it easier to run.  


Upload binary
----------
>$ avrdude -v -q -p m2560 -c wiring -P /dev/ttyUSB0 -D -U flash:w:/path/to/image.hex:i


Configuration after upload
==========


PID tuning
---------------
Start parts fan at 100%  
>M106 S255

	[...]
	Send: M106 S255
	Recv: ok
	[...]

Start tuning  
>M303 E0 S205 C8

	[...]
	Recv:  bias: 169 d: 85 min: 202.71 max: 207.81 Ku: 42.41 Tu: 27.20
	Recv:  Classic PID
	Recv:  Kp: 25.44 Ki: 1.87 Kd: 86.50
	Recv: PID Autotune finished! Put the last Kp, Ki and Kd constants from below into Configuration.h
	Recv: #define DEFAULT_Kp 25.44
	Recv: #define DEFAULT_Ki 1.87
	Recv: #define DEFAULT_Kd 86.50
	Recv: ok
	[...]
	
Enter new values  
>M301 P25.44 I1.87 D86.50

	[...]
	Send: M301 P25.44 I1.87 D86.50
	Recv: echo: p:25.44 i:1.87 d:86.50
	Recv: ok
	[...]
	
Save to EEPROM  
>M500

	[...]
	Send: M500
	Recv: echo:Settings Stored (657 bytes; crc 43001)
	Recv: ok
	[...]


Set Z-offset
---------------
View current offset  
>M851

	[...]
	Send: M851
	Recv: Probe Offset X20.00 Y2.00 Z-0.90
	Recv: ok
	[...]
	
Set new Z offset  
>M851 Z-0.8

	[...]
	Send: M851 Z-0.8
	Recv: echo:Probe Z Offset: -0.80
	Recv: ok
	[...]
		
Save new value to EEPROM  
>M500

Higher value -> smaller distance from bed  
The above example will decrease the distance from the bed, ie. the gap between nozzle and bed will be smaller.  

This can of course also be done from the LCD-display.  


Skew factor
----------
Adapted from https://github.com/MarlinFirmware/Configurations/blob/import-2.0.x/config/examples/Geeetech/Prusa%20i3%20Pro%20B/bltouch/README.md  

The skew factor must be adjusted for each printer:

- First, uncomment `#define XY_SKEW_FACTOR 0.0`, if commented

1445  

	  #define XY_SKEW_FACTOR 0.0

- Compile and upload the firmware.
- Then, print [YACS (Yet Another Calibration Square)](https://www.thingiverse.com/thing:2563185). Hint, scale it considering a margin for brim (if used). The larger, the better to make error measurements.
- Measure the printed part according to the comments in the example configuration file, and set `XY_DIAG_AC`, `XY_DIAG_BD` and `Y_SIDE_AD`.

1439  

	  #define XY_DIAG_AC 282.8427124746
	  #define XY_DIAG_BD 282.8427124746
	  #define XY_SIDE_AD 200
	  
- Comment `#define XY_SKEW_FACTOR 0.0` again.
	
1445  

	  //#define XY_SKEW_FACTOR 0.0

- Compile and upload again.


Misc g-code
==========
Settings
----------
>M503 ; view current settings and parameters

>M500 ; store settings to EEPROM

>M502 ; load settings from EEPROM


BLTouch
---------------
>M280 P0 S10 ; pushes the pin down  

>M280 P0 S90 ; pulls the pin up  

>M280 P0 S120 ; Self test – keeps going until you do pin up/down or release alarm  

>M280 P0 S160 ; Release alarm  


Homing and leveling
----------
>G28 ; home all axes

>G29 ; do bed leveling


Below is just for my own reference
==========
Other PID values I've tried:  
>M301 P32.86 I2.59 D104.31 ; 1.1.8, with fan off
>M301 P33.26 I2.49 D111.03 ; 2.0.7.2, with fan off
>M301 P28.44 I2.12 D95.53 ; 2.0.7.2, fan on
>M301 P23.26 I1.72 D78.61 ; 2.0.7.2, fan off, 200 degrees
>M301 P23.12 I1.72 D77.65 ; 2.0.7.2, fan on, 200 degrees
>M301 P22.26 I1.69 D73.38 ; 2.0.7.2, fan on, new parts cooler



