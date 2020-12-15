## Firmware tinkering on Marlin-2.0.7.2 for Geeetech I3 Pro B

Further down in this document are instructions on how to trim, set up and install firmware on your printer.  

Please scroll through whole document so you don't miss anything. :-)  

Instructions below are run on a Linux system.  


Changes from original firmware release
==========
These are my changes from the vanilla firmware.  
Some things will perhaps have to be adapted to fit your printer setup.  

Makefile
----------
Line 60  

	HARDWARE_MOTHERBOARD ?= 1315
	
configuration.h
----------
Line 73  

	#define STRING_CONFIG_H_AUTHOR "jonsag" // Who made the changes.
	
130  

	  #define MOTHERBOARD BOARD_GT2560_REV_A_PLUS
	
134  

	#define CUSTOM_MACHINE_NAME "Geeetech i3 Pro B"

426  

	#define TEMP_SENSOR_BED 1
	
476  

	#define BED_MAXTEMP      125

498-  

	    #define DEFAULT_Kp_LIST {  22.39,  22.39 }
	    #define DEFAULT_Ki_LIST {   1.91,   1.91 }
	    #define DEFAULT_Kd_LIST { 65.58, 65.58 }

502-  

	    #define DEFAULT_Kp  22.39
	    #define DEFAULT_Ki   1.91
	    #define DEFAULT_Kd 65.58

596  

	//#define THERMAL_PROTECTION_CHAMBER // Enable thermal protection for the heated chamber
	
681-  

	#define X_DRIVER_TYPE  A4988
	#define Y_DRIVER_TYPE  A4988
	#define Z_DRIVER_TYPE  A4988

689  

	#define E0_DRIVER_TYPE A4988
	
744-  

	#define PRO_B_WITH_LEADSCREW
	#if ENABLED(PRO_B_WITH_LEADSCREW)       // T8 leadscrew version
	  #define DEFAULT_AXIS_STEPS_PER_UNIT   { 81.5, 81.5, 400.69, 108 }
	#else                                   // M8 threaded rod version
	  #define DEFAULT_AXIS_STEPS_PER_UNIT   { 78.74, 78.74, 2560, 105 }
	#endif
	
756  

	#define DEFAULT_MAX_FEEDRATE          { 400, 400, 2, 45 }

769  

	#define DEFAULT_MAX_ACCELERATION      { 5000, 5000, 50, 5000 }
	
784-  

	#define DEFAULT_ACCELERATION          1000    // X, Y, Z and E acceleration for printing moves
	#define DEFAULT_RETRACT_ACCELERATION  2000    // E acceleration for retracts
	#define DEFAULT_TRAVEL_ACCELERATION   1000    // X, Y, Z acceleration for travel (non printing) moves
	
833  

	#define S_CURVE_ACCELERATION
	
907-  

	#define BLTOUCH
	#if ENABLED(BLTOUCH)
	  #define BLTOUCH_DELAY 375   // (ms) Enable and increase if 	needed
	#endif

997  

	#define NOZZLE_TO_PROBE_OFFSET { 20, 2, -0.9}

1050  

	#define Z_MIN_PROBE_REPEATABILITY_TEST
	
1097  

	#define INVERT_X_DIR true

1104  

	#define INVERT_E0_DIR true
	
1133-  

	#define X_BED_SIZE 186
	#define Y_BED_SIZE 167
	
1137-  

	#define X_MIN_POS 10
	#define Y_MIN_POS -10

1140-  

	#define X_MAX_POS (X_MIN_POS + X_BED_SIZE)
	#define Y_MAX_POS (-Y_MIN_POS + Y_BED_SIZE))
	#define Z_MAX_POS 185
	
1244  

	#define AUTO_BED_LEVELING_LINEAR
	
1253  

	#define RESTORE_LEVELING_AFTER_G28
	    
1322  

	  #define MESH_EDIT_GFX_OVERLAY   // Display a graphics overlay while editing the mesh
	  
1352  

	#define LCD_BED_LEVELING
	
1361  

	#define LEVEL_BED_CORNERS
	  
1367  

	  #define LEVEL_CENTER_TOO              // Move to the center after the last corner
	  
1396  

	#define Z_SAFE_HOMING
	
1440  

	#define SKEW_CORRECTION
	
1464  

	  #define SKEW_CORRECTION_GCODE
	  
1482-  

	#define EEPROM_SETTINGS     // Persistent storage with M500 and M501
	#define DISABLE_M503        // Saves ~2700 bytes of PROGMEM. Disable for release!
	
1514  

	#define PREHEAT_1_TEMP_HOTEND 205
	
1518  

	#define PREHEAT_2_LABEL       "PETG"
	#define PREHEAT_2_TEMP_HOTEND 235
	#define PREHEAT_2_TEMP_BED    85

1647  

	#define PRINTCOUNTER

1735  

	#define SDSUPPORT

1752  

	#define SD_CHECK_AND_RETRY

1815  

	#define INDIVIDUAL_AXIS_HOMING_MENU
	
1823  

	#define SPEAKER

1832-  

	#define LCD_FEEDBACK_FREQUENCY_DURATION_MS 2
	#define LCD_FEEDBACK_FREQUENCY_HZ 5000

1846  

	#define REPRAP_DISCOUNT_SMART_CONTROLLER
	
1901  

	#define ULTRA_LCD

	
Other possible changes in configuration.h
==========

Thermal protection chamber
----------
596  

	#define THERMAL_PROTECTION_CHAMBER // Enable thermal protection for the heated chamber


Extra probing
----------
1021  

	#define MULTIPLE_PROBING 3
	
Enable M503 reporting
----------
1483  

	//#define DISABLE_M503        // Saves ~2700 bytes of PROGMEM. Disable for release!

	  

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
----- This part is under construction -----  

This is NOT your command
>$ avrdude -v -p atmega328p -c arduino -P /dev/ttyUSB0 -b 57600 -D -U flash:w:/home/pi/avrdude/Blink.hex:i


Configuration after upload
==========
View current settings and parameters  
>M503

Note:  
Disabled on line 1483 in Configuration.h  

Change to  

	//#define DISABLE_M503        // Saves ~2700 bytes of PROGMEM. Disable for release!

to enable again.  


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
	Recv: echo:Probe Z Offset: -0.95
	Recv: ok
	[...]
	
Set new offset  
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
BLTouch
---------------
>M280 P0 S10 ; pushes the pin down  

>M280 P0 S90 ; pulls the pin up  

>M280 P0 S120 ; Self test – keeps going until you do pin up/down or release alarm  

>M280 P0 S160 ; Release alarm  


Homing and levelling
----------
>G28 ; home all axes

>G29 ; bed levelling

