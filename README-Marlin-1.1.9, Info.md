#Firmware tinkering on Marlin for Geeetech I3 Pro B

Configuration.h
===============

Motherboard selection, 131-135
---------------
	// The following define selects which electronics board you have.
	// Please choose the name from boards.h that matches your setup
	#ifndef MOTHERBOARD
	  #define MOTHERBOARD BOARD_GT2560_REV_A_PLUS
	#endif
	
Custom name, 137-139
---------------
	// Optional custom name for your RepStrap or other custom machine
	// Displayed in the LCD "Ready" message
	#define CUSTOM_MACHINE_NAME "Geeetech I3 Pro B""

Filament diameter, 151-152
---------------
	// Generally expected filament diameter (1.75, 2.85, 3.0, ...). Used for Volumetric, Filament Width Sensor, etc.
	#define DEFAULT_NOMINAL_FILAMENT_DIA 1.75

Temperature sensors, 264-319
---------------
	/**
	 * --NORMAL IS 4.7kohm PULLUP!-- 1kohm pullup can be used on hotend sensor, using correct resistor and table
	 *
	 * Temperature sensors available:
	...
	...
	...
	 */
	#define TEMP_SENSOR_0 1
	#define TEMP_SENSOR_1 0
	#define TEMP_SENSOR_2 0
	#define TEMP_SENSOR_3 0
	#define TEMP_SENSOR_4 0
	#define TEMP_SENSOR_BED 1
	#define TEMP_SENSOR_CHAMBER 0
	
Min temps, 340-348
---------------
	// The minimal temperature defines the temperature below which the heater will not be enabled It is used
	// to check that the wiring to the thermistor is not broken.
	// Otherwise this would lead to the heater being powered on all the time.
	#define HEATER_0_MINTEMP 8
	#define HEATER_1_MINTEMP 5
	#define HEATER_2_MINTEMP 5
	#define HEATER_3_MINTEMP 5
	#define HEATER_4_MINTEMP 5
	#define BED_MINTEMP 8

Steps/mm, 606-611
---------------
	/**
	 * Default Axis Steps Per Unit (steps/mm)
	 * Override with M92
	 *                                      X, Y, Z, E0 [, E1[, E2[, E3[, E4]]]]
	 */
	#define DEFAULT_AXIS_STEPS_PER_UNIT   { 81.5, 81.5, 400.69, 108 }
	
Max feed rate, 613-618
---------------
	/**
	 * Default Max Feed Rate (mm/s)
	 * Override with M203
	 *                                      X, Y, Z, E0 [, E1[, E2[, E3[, E4]]]]
	 */
	#define DEFAULT_MAX_FEEDRATE          { 400, 400, 2, 45 }
	
Max accceleration, 620-626
---------------
	/**
	 * Default Max Acceleration (change/s) change = mm/s
	 * (Maximum start speed for accelerated moves)
	 * Override with M201
	 *                                      X, Y, Z, E0 [, E1[, E2[, E3[, E4]]]]
	 */
	#define DEFAULT_MAX_ACCELERATION      { 5000, 5000, 50, 5000 }
	
Default acceleration, 628-638
---------------
	/**
	 * Default Acceleration (change/s) change = mm/s
	 * Override with M204
	 *
	 *   M204 P    Acceleration
	 *   M204 R    Retract Acceleration
	 *   M204 T    Travel Acceleration
	 */
	#define DEFAULT_ACCELERATION          1000    // X, Y, Z and E acceleration for printing moves
	#define DEFAULT_RETRACT_ACCELERATION  2000    // E acceleration for retracts
	#define DEFAULT_TRAVEL_ACCELERATION   1000    // X, Y, Z acceleration for travel (non printing) moves

Default jerk, 640-651
---------------
	/**
	 * Default Jerk (mm/s)
	 * Override with M205 X Y Z E
	 *
	 * "Jerk" specifies the minimum speed change that requires acceleration.
	 * When changing speed and direction, if the difference is less than the
	 * value set here, it may happen instantaneously.
	 */
	#define DEFAULT_XJERK                 20.0
	#define DEFAULT_YJERK                 20.0
	#define DEFAULT_ZJERK                 0.4
	#define DEFAULT_EJERK                 5.0
	
Bltouch, 727-733
---------------
	/**
	 * The BLTouch probe uses a Hall effect sensor and emulates a servo.
	 */
	#define BLTOUCH
	#if ENABLED(BLTOUCH)
	  #define BLTOUCH_DELAY 375   // (ms) Enable and increase if needed
	#endif

Bltouch probe offsets, 760-781
---------------	
	/**
	 *   Z Probe to nozzle (X,Y) offset, relative to (0, 0).
	 *   X and Y offsets must be integers.
	 *
	 *   In the following example the X and Y offsets are both positive:
	 *   #define X_PROBE_OFFSET_FROM_EXTRUDER 10
	 *   #define Y_PROBE_OFFSET_FROM_EXTRUDER 10
	 *
	 *      +-- BACK ---+
	 *      |           |
	 *    L |    (+) P  | R <-- probe (20,20)
	 *    E |           | I
	 *    F | (-) N (+) | G <-- nozzle (10,10)
	 *    T |           | H
	 *      |    (-)    | T
	 *      |           |
	 *      O-- FRONT --+
	 *    (0,0)
	 */
	#define X_PROBE_OFFSET_FROM_EXTRUDER -40  // X offset: -left  +right  [of the nozzle]
	#define Y_PROBE_OFFSET_FROM_EXTRUDER 0  // Y offset: -front +behind [the nozzle]
	#define Z_PROBE_OFFSET_FROM_EXTRUDER -0.9   // Z offset: -below +above  [the nozzle]

Speed between probes, 786-787
---------------
	// X and Y axis travel speed (mm/m) between probes
	#define XY_PROBE_SPEED 8000

Feedrate for probing, 792-793
---------------
	// Feedrate (mm/m) for the "accurate" probe of each point
	#define Z_PROBE_SPEED_SLOW (Z_PROBE_SPEED_FAST )

Z clearance, 800-817
---------------
	/**
	 * Z probes require clearance when deploying, stowing, and moving between
	 * probe points to avoid hitting the bed and other hardware.
	 * Servo-mounted probes require extra space for the arm to rotate.
	 * Inductive probes need space to keep from triggering early.
	 *
	 * Use these settings to specify the distance (mm) to raise the probe (or
	 * lower the bed). The values set here apply over and above any (negative)
	 * probe Z Offset set with Z_PROBE_OFFSET_FROM_EXTRUDER, M851, or the LCD.
	 * Only integer values >= 1 are valid here.
	 *
	 * Example: `M851 Z-5` with a CLEARANCE of 4  =>  9mm from bed to nozzle.
	 *     But: `M851 Z+1` with a CLEARANCE of 2  =>  2mm from bed to nozzle.
	 */
	#define Z_CLEARANCE_DEPLOY_PROBE   3 // Z Clearance for Deploy/Stow
	#define Z_CLEARANCE_BETWEEN_PROBES 2 // Z Clearance between probe points
	#define Z_CLEARANCE_MULTI_PROBE    2 // Z Clearance between multiple probes
	#define Z_AFTER_PROBING            5 // Z position after probing is done

	
Stepper directions, 850-862
---------------
	// Invert the stepper direction. Change (or reverse the motor connector) if an axis goes the wrong way.
	#define INVERT_X_DIR true
	#define INVERT_Y_DIR true
	#define INVERT_Z_DIR false

	// @section extruder

	// For direct drive extruder v9 set to true, for geared extruder set to false.
	#define INVERT_E0_DIR true
	#define INVERT_E1_DIR false
	#define INVERT_E2_DIR false
	#define INVERT_E3_DIR false
	#define INVERT_E4_DIR false
	
Bed size and travel limits, 881-891
---------------
	// The size of the print bed
	#define X_BED_SIZE 196
	#define Y_BED_SIZE 192

	// Travel limits (mm) after homing, corresponding to endstop positions.
	#define X_MIN_POS 5
	#define Y_MIN_POS 0
	#define Z_MIN_POS 0
	#define X_MAX_POS X_BED_SIZE + X_MIN_POS
	#define Y_MAX_POS Y_BED_SIZE
	#define Z_MAX_POS 185
	
Bed levelling, 943-980
---------------
	/**
	 * Choose one of the options below to enable G29 Bed Leveling. The parameters
	 * and behavior of G29 will change depending on your selection.
	 *
	 *  If using a Probe for Z Homing, enable Z_SAFE_HOMING also!
	...
	...
	...
	//#define AUTO_BED_LEVELING_3POINT
	#define AUTO_BED_LEVELING_LINEAR
	//#define AUTO_BED_LEVELING_BILINEAR
	//#define AUTO_BED_LEVELING_UBL
	//#define MESH_BED_LEVELING
	
Leveling disabled, 982-986
---------------
	/**
	 * Normally G28 leaves leveling disabled on completion. Enable
	 * this option to have G28 restore the prior leveling state.
	 */
	#define RESTORE_LEVELING_AFTER_G28

Enable mesh validation, 1007-1016
---------------
	  /**
	   * Enable the G26 Mesh Validation Pattern tool.
	   */
	  #define G26_MESH_VALIDATION
	  #if ENABLED(G26_MESH_VALIDATION)
	    #define MESH_TEST_NOZZLE_SIZE    0.4  // (mm) Diameter of primary nozzle.
	    #define MESH_TEST_LAYER_HEIGHT   1.5  // (mm) Default layer height for the G26 Mesh Validation Tool.
	    #define MESH_TEST_HOTEND_TEMP  230.0  // (°C) Default nozzle temperature for the G26 Mesh Validation Tool.
	    #define MESH_TEST_BED_TEMP      80.0  // (°C) Default bed temperature for the G26 Mesh Validation Tool.
	  #endif

Options for linear leveling, 1020-1052
---------------
	#if ENABLED(AUTO_BED_LEVELING_LINEAR) || ENABLED(AUTO_BED_LEVELING_BILINEAR)

	  // Set the number of grid points per dimension.
	  #define GRID_MAX_POINTS_X 3
	  #define GRID_MAX_POINTS_Y GRID_MAX_POINTS_X

	  // Set the boundaries for probing (where the probe can reach).
	  #define LEFT_PROBE_BED_POSITION 10
	  #define RIGHT_PROBE_BED_POSITION (X_BED_SIZE - MIN_PROBE_EDGE - X_PROBE_OFFSET_FROM_EXTRUDER) 
	  #define FRONT_PROBE_BED_POSITION 10
	  //#define BACK_PROBE_BED_POSITION 143
	  #define BACK_PROBE_BED_POSITION (Y_BED_SIZE - MIN_PROBE_EDGE + Y_PROBE_OFFSET_FROM_EXTRUDER -3)

	  // Probe along the Y axis, advancing X after each column
	  //#define PROBE_Y_FIRST

	  #if ENABLED(AUTO_BED_LEVELING_BILINEAR)

	    // Beyond the probed grid, continue the implied tilt?
	    // Default is to maintain the height of the nearest edge.
	    #define EXTRAPOLATE_BEYOND_GRID

	    //
	    // Experimental Subdivision of the grid by Catmull-Rom method.
	    // Synthesizes intermediate points to produce a more detailed mesh.
	    //
	    //#define ABL_BILINEAR_SUBDIVISION
	    #if ENABLED(ABL_BILINEAR_SUBDIVISION)
	      // Number of subdivisions between probe points
	      #define BILINEAR_SUBDIVISIONS 3
	    #endif

	  #endif

Level bed corners, 1013-1017
---------------
	#if ENABLED(LEVEL_BED_CORNERS)
	  #define LEVEL_CORNERS_INSET 30    // (mm) An inset for corner leveling
	  #define LEVEL_CORNERS_Z_HOP  4.0  // (mm) Move nozzle up before moving between corners
	  //#define LEVEL_CENTER_TOO        // Move to the center after the last corner
	#endif

Z safe homing, 1137-1156
---------------
	// Use "Z Safe Homing" to avoid homing with a Z probe outside the bed area.
	//
	// With this feature enabled:
	//
	// - Allow Z homing only after X and Y homing AND stepper drivers still enabled.
	// - If stepper drivers time out, it will need X and Y homing again before Z homing.
	// - Move the Z probe (or nozzle) to a defined XY point before Z Homing when homing all axes (G28).
	// - Prevent Z homing when the Z probe is outside bed area.
	//
	#define Z_SAFE_HOMING
	
Homing speeds, 1153-1155
---------------
	// Homing speeds (mm/m)
	#define HOMING_FEEDRATE_XY (60*60)
	#define HOMING_FEEDRATE_Z  (60*60)

M500 and M501 commands, 1221-1230
---------------
	// EEPROM
	//
	// The microcontroller can store settings in the EEPROM, e.g. max velocity...
	// M500 - stores parameters in EEPROM
	// M501 - reads parameters from EEPROM (if you need reset them after you changed them temporarily).
	// M502 - reverts to the default "factory settings".  You still need to store them in EEPROM afterwards if you want to.
	//
	#define EEPROM_SETTINGS // Enable for M500 and M501 commands
	//#define DISABLE_M503    // Saves ~2700 bytes of PROGMEM. Disable for release!
	#define EEPROM_CHITCHAT   // Give feedback on EEPROM commands. Disable to save PROGMEM.

Host keepalive, 1233-1240
---------------
	// Host Keepalive
	//
	// When enabled Marlin will send a busy status message to the host
	// every couple of seconds when it can't accept commands.
	//
	#define HOST_KEEPALIVE_FEATURE        // Disable this if your host doesn't like keepalive messages
	#define DEFAULT_KEEPALIVE_INTERVAL 4  // Number of seconds between "busy" messages. Set with M113.
	#define BUSY_WHILE_HEATING            // Some hosts require "busy" messages even during heating

Preheating, 2559-1266
---------------
	// Preheat Constants
	#define PREHEAT_1_TEMP_HOTEND 180
	#define PREHEAT_1_TEMP_BED     60
	#define PREHEAT_1_FAN_SPEED     0 // Value from 0 to 255

	#define PREHEAT_2_TEMP_HOTEND 225
	#define PREHEAT_2_TEMP_BED    90
	#define PREHEAT_2_FAN_SPEED     0 // Value from 0 to 255
	
Nozzle park, 1281-1286
---------------
	#if ENABLED(NOZZLE_PARK_FEATURE)
	  // Specify a park position as { X, Y, Z }
	  #define NOZZLE_PARK_POINT { (X_MIN_POS + 10), (Y_MAX_POS - 10), 20 }
	  #define NOZZLE_PARK_XY_FEEDRATE 100   // X and Y axes feedrate in mm/s (also used for delta printers Z axis)
	  #define NOZZLE_PARK_Z_FEEDRATE 100      // Z axis feedrate in mm/s (not used for delta printers)
	#endif

SD support, 1424-1431
---------------
	/**
	 * SD CARD
	 *
	 * SD Card support is disabled by default. If your controller has an SD slot,
	 * you must uncomment the following option or it won't work.
	 *
	 */
	#define SDSUPPORT

Feedback sound, 1514-1521
---------------
	// The duration and frequency for the UI feedback sound.
	// Set these to 0 to disable audio feedback in the LCD menus.
	//
	// Note: Test audio output with the G-Code:
	//  M300 S<frequency Hz> P<duration ms>
	//
	#define LCD_FEEDBACK_FREQUENCY_DURATION_MS 0
	#define LCD_FEEDBACK_FREQUENCY_HZ 0

Smart controller, 1533
---------------
	#define REPRAP_DISCOUNT_SMART_CONTROLLERR

SAV OLEd support, 1637-1643
---------------
	// SAV OLEd LCD module support using either SSD1306 or SH1106 based LCD modules
	//
	//#define SAV_3DGLCD
	#if ENABLED(SAV_3DGLCD)
	  //#define U8GLIB_SSD1306
	  #define U8GLIB_SH1106
	#endif
	
Number of servos, 1920-1927
---------------
	/**
	 * Number of servos
	 *
	 * For some servo-related options NUM_SERVOS will be set automatically.
	 * Set this manually if there are extra servos needing manual control.
	 * Leave undefined or set to 0 to entirely disable the servo subsystem.
	 */
	#define NUM_SERVOS 1 // Servo index starts with 0 for M280 command


pins_GT2560_REV_A_PLUS.h
===============

Bltouch, 31-35
---------------
	#if ENABLED(BLTOUCH)
	  #define SERVO0_PIN  11
	#else
	  #define SERVO0_PIN  11
	#endif







