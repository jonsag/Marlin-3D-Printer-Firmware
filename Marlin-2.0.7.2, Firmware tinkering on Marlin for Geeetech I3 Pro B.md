#Firmware tinkering on Marlin-2.0.7.2 for Geeetech I3 Pro B

Line numbers are after the changes  

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

	#define CUSTOM_MACHINE_NAME "GeeeTech I3 Pro B"

426  

	#define TEMP_SENSOR_BED 1
	
476  

	#define BED_MAXTEMP      125

596  

	//#define THERMAL_PROTECTION_CHAMBER // Enable thermal protection for the heated chamber
	
681-  

	#define X_DRIVER_TYPE  A4988
	#define Y_DRIVER_TYPE  A4988
	#define Z_DRIVER_TYPE  A4988

689  

	#define E0_DRIVER_TYPE A4988
	
744  

	#define DEFAULT_AXIS_STEPS_PER_UNIT   { 81.5, 81.5, 400.69, 108 }
	
751  

	#define DEFAULT_MAX_FEEDRATE          { 400, 400, 2, 45 }

764  

	#define DEFAULT_MAX_ACCELERATION      { 3000, 3000, 100, 10000 } // { 5000, 5000, 75, 5000 }
	
779-  

	#define DEFAULT_ACCELERATION          3000    // X, Y, Z and E acceleration for printing moves // 1000
	#define DEFAULT_RETRACT_ACCELERATION  3000    // E acceleration for retracts // 2000
	#define DEFAULT_TRAVEL_ACCELERATION   3000    // X, Y, Z acceleration for travel (non printing) moves
	
793-  

	 #define DEFAULT_XJERK                 5.0 // 10.0
	 #define DEFAULT_YJERK                 5.0 // 10.0
	 #define DEFAULT_ZJERK                 0.3
	 
805  

	#define DEFAULT_EJERK    4.0  // May be used by Linear Advance // 5.0
	
828  

	#define S_CURVE_ACCELERATION
	
902-  

	#define BLTOUCH
	#if ENABLED(BLTOUCH)
	  #define BLTOUCH_DELAY 375   // (ms) Enable and increase if 	needed
	#endif

992  

	#define NOZZLE_TO_PROBE_OFFSET { 20, 2, -1.6 }
	
1045  

	#define Z_MIN_PROBE_REPEATABILITY_TEST
	
1092  

	#define INVERT_X_DIR true

1099  

	#define INVERT_E0_DIR true
	
1128-  

	#define X_BED_SIZE 196
	#define Y_BED_SIZE 192
	
1132  

	#define X_MIN_POS 5
	
1135  

	#define X_MAX_POS (-X_MIN_POS+X_BED_SIZE)

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
	
1477-  

	#define EEPROM_SETTINGS     // Persistent storage with M500 and M501
	#define DISABLE_M503        // Saves ~2700 bytes of PROGMEM. Disable for release!
	
1509  

	#define PREHEAT_1_TEMP_HOTEND 205
	
1513  

	#define PREHEAT_2_LABEL       "PETG"
	#define PREHEAT_2_TEMP_HOTEND 235
	#define PREHEAT_2_TEMP_BED    85

1730  

	#define SDSUPPORT

1810  

	#define INDIVIDUAL_AXIS_HOMING_MENU
	
1818  

	#define SPEAKER

1827  

	#define LCD_FEEDBACK_FREQUENCY_DURATION_MS 0
	#define LCD_FEEDBACK_FREQUENCY_HZ 0

1841  

	#define REPRAP_DISCOUNT_SMART_CONTROLLER
	
1896  

	#define ULTRA_LCD
	







