## Firmware tinkering on Marlin-2.0.7.2 for Geeetech I3 Pro B

Further down in this document are instructions on how to trim, set up and install firmware on your printer.  

Please scroll through whole document so you don't miss anything. :-)  

Changes from vanilla firmware
==========
These are the changes from the vanilla firmware.  
Some things will perhaps have to be adapted to fit your printer setup.  

Line numbers are sometimes not exact, and after the changes  

Makefile
----------
60  

	HARDWARE_MOTHERBOARD ?= 1315
	
configuration.h
----------
74  

	#define STRING_CONFIG_H_AUTHOR "jonsag" // Who made the changes.
	
130  

	  #define MOTHERBOARD BOARD_GT2560_REV_A_PLUS
	
134  

	#define CUSTOM_MACHINE_NAME "GeeeTech i3 Pro B"

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
	#if ENABLED(PRO_B_WITH_LEADSCREW)       // M8 leadscrew version
	  #define DEFAULT_AXIS_STEPS_PER_UNIT   { 81.5, 81.5, 400.69, 108 }
	#else                                   // M8 threaded rod version
	  #define DEFAULT_AXIS_STEPS_PER_UNIT   { 78.74, 78.74, 2560, 105 }
	#endif
	
756  

	#define DEFAULT_MAX_FEEDRATE          { 400, 400, 2, 45 }

769  

	#define DEFAULT_MAX_ACCELERATION      { 3000, 3000, 100, 10000 } // { 5000, 5000, 75, 5000 }
	
784-  

	#define DEFAULT_ACCELERATION          3000    // X, Y, Z and E acceleration for printing moves // 1000
	#define DEFAULT_RETRACT_ACCELERATION  3000    // E acceleration for retracts // 2000
	#define DEFAULT_TRAVEL_ACCELERATION   3000    // X, Y, Z acceleration for travel (non printing) moves
	
798-  

	 #define DEFAULT_XJERK                 5.0 // 10.0
	 #define DEFAULT_YJERK                 5.0 // 10.0
	 #define DEFAULT_ZJERK                 0.3
	 
810  

	#define DEFAULT_EJERK    4.0  // May be used by Linear Advance // 5.0
	
833  

	#define S_CURVE_ACCELERATION
	
908-  

	#define BLTOUCH
	#if ENABLED(BLTOUCH)
	  #define BLTOUCH_DELAY 375   // (ms) Enable and increase if 	needed
	#endif

997  

	#define NOZZLE_TO_PROBE_OFFSET { 20, 2, -0.9}

1001  

	#define PROBING_MARGIN 10

1045  

	#define Z_MIN_PROBE_REPEATABILITY_TEST
	
1092  

	#define INVERT_X_DIR true

1099  

	#define INVERT_E0_DIR true
	
1133-  

	#define X_BED_SIZE 186
	#define Y_BED_SIZE 177
	
1137-  

	#define X_MIN_POS 10
	#define Y_MIN_POS -10

1140-  

	#define X_MAX_POS (X_MIN_POS + X_BED_SIZE)
	#define Y_MAX_POS (-Y_MIN_POS + Y_BED_SIZE))
	
1137  

	#define Z_MAX_POS 185
	
1239  

	#define AUTO_BED_LEVELING_LINEAR
	
1248  

	#define RESTORE_LEVELING_AFTER_G28
	    
1277  

	    #define MESH_TEST_BED_TEMP      65    // (°C) Default bed temperature for the G26 Mesh Validation Tool.
	    
1317  

	  #define MESH_EDIT_GFX_OVERLAY   // Display a graphics overlay while editing the mesh
	  
1347  

	#define LCD_BED_LEVELING
	
1356  

	#define LEVEL_BED_CORNERS
	
1359  

	  #define LEVEL_CORNERS_INSET_LFRB { 60, 60, 60, 60 } // (mm) Left, Front, Right, Back insets
	  
1362  

	  #define LEVEL_CENTER_TOO              // Move to the center after the last corner
	  
1391  

	#define Z_SAFE_HOMING
	
1440  

	#define SKEW_CORRECTION
	
1464  

	  #define SKEW_CORRECTION_GCODE
	  
1477-  

	#define EEPROM_SETTINGS     // Persistent storage with M500 and M501
	#define DISABLE_M503        // Saves ~2700 bytes of PROGMEM. Disable for release!
	
1509  

	#define PREHEAT_1_TEMP_HOTEND 205
	
1513  

	#define PREHEAT_2_LABEL       "PETG"
	#define PREHEAT_2_TEMP_HOTEND 235
	#define PREHEAT_2_TEMP_BED    85

1647  

	#define PRINTCOUNTER

1730  

	#define SDSUPPORT

1752  

	#define SD_CHECK_AND_RETRY

1810  

	#define INDIVIDUAL_AXIS_HOMING_MENU
	
1818  

	#define SPEAKER

1827  

	#define LCD_FEEDBACK_FREQUENCY_DURATION_MS 0
	#define LCD_FEEDBACK_FREQUENCY_HZ 0

1832-  

	#define LCD_FEEDBACK_FREQUENCY_DURATION_MS 2
	#define LCD_FEEDBACK_FREQUENCY_HZ 5000
1841  

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
	  

Compiling
==========
Download Arduino IDE 1.8.x from https://www.arduino.cc/en/software  

Open Arduino IDE and open /path/to/Marlin.ini  

Select board:  
Tools -> Board: ... -> Arduino AVR Boards -> Arduino 2560 or Mega 2560  

Select processor:  
Tools -> Processor: ... -> ATmega2560 (Mega 2560)  
 
Select programmer: 
Tools -> Programmer: ... -> AVRIPS mkII  

Also set port:  
Tools -> /dev/ttyUSB0 or whatever...  

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


Configuration after upload
==========
View current settings and parameters  
>M503


PID tuning
---------------
Start fan at 100%  
>M106 S255

Start tuning
>M303 E0 S200 C8

This will return something like:  

	bias: 174 d: 80 min: 197.27 max: 202.81 Ku: 36.77 Tu: 41.62
	Classic PIDRecv:  Kp: 22.06 Ki: 1.06 Kd: 114.78
	PID Autotune finished! Put the last Kp, Ki and Kd constants from below into Configuration.h
	#define  DEFAULT_Kp 22.06
	#define  DEFAULT_Ki 1.06
	#define  DEFAULT_Kd 114.78
	
Enter new values with:
>M301 P22.06 I1.06 D114.78

Save to EEPROM with:
>M500


Set Z-offset
---------------
View current offset  
>M851

Returns  

	Send: M851
	Recv: echo:Probe Z Offset: -0.95
	Recv: ok
	
Set new offset  
>M851 Z-0.8

Returns  

	Send: M851 Z-0.8
	Recv: echo:Probe Z Offset: -0.80
	Recv: ok
	
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

