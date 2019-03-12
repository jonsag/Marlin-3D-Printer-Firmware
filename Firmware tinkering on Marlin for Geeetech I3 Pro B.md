#Firmware tinkering on Marlin for Geeetech I3 Pro B

Configuration.h
===============

Motherboard selection, 119-123
---------------
	// The following define selects which electronics board you have.
	// Please choose the name from boards.h that matches your setup
	#ifndef MOTHERBOARD
	  #define MOTHERBOARD BOARD_GT2560_REV_A_PLUS
	#endif
	
Custom name, 125-127
---------------
	// Optional custom name for your RepStrap or other custom machine
	// Displayed in the LCD "Ready" message
	#define CUSTOM_MACHINE_NAME "Geeetech i3 Pro B"

Filament diameter, 139-140
---------------
	// Generally expected filament diameter (1.75, 2.85, 3.0, ...). Used for Volumetric, Filament Width Sensor, etc.
	#define DEFAULT_NOMINAL_FILAMENT_DIA 1.75

Temperature sensors, 243-294
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
	#define TEMP_SENSOR_BED 11
	
Min temps, 315-323
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

Steps/mm, 527-533
---------------
	/**
	 * Default Axis Steps Per Unit (steps/mm)
	 * Override with M92
	 *                                      X, Y, Z, E0 [, E1[, E2[, E3[, E4]]]]
	 */
	//#define DEFAULT_AXIS_STEPS_PER_UNIT   { 81.5, 81.5, 2577.46, 94 }
	#define DEFAULT_AXIS_STEPS_PER_UNIT   { 81.5, 81.5, 400.69, 93 }

Max feed rate, 534-539
---------------
	/**
	 * Default Max Feed Rate (mm/s)
	 * Override with M203
	 *                                      X, Y, Z, E0 [, E1[, E2[, E3[, E4]]]]
	 */
	#define DEFAULT_MAX_FEEDRATE          { 400, 400, 2, 45 }

Max accceleration, 541-547
---------------
	/**
	 * Default Max Acceleration (change/s) change = mm/s
	 * (Maximum start speed for accelerated moves)
	 * Override with M201
	 *                                      X, Y, Z, E0 [, E1[, E2[, E3[, E4]]]]
	 */
	#define DEFAULT_MAX_ACCELERATION      { 5000, 5000, 50, 5000 }

Default acceleration, 549-559
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

Default jerk, 572-561
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
	#define DEFAULT_ZJERK                  0.4
	#define DEFAULT_EJERK                  5.0
	
Bltouch, 637-643
---------------
	/**
	 * The BLTouch probe uses a Hall effect sensor and emulates a servo.
	 */
	#define BLTOUCH
	#if ENABLED(BLTOUCH)
	  #define BLTOUCH_DELAY 375   // (ms) Enable and increase if needed
	#endif

Bltouch probe offsets, 667-688
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
	#define Y_PROBE_OFFSET_FROM_EXTRUDER -0  // Y offset: -front +behind [the nozzle]
	#define Z_PROBE_OFFSET_FROM_EXTRUDER -0.9  // Z offset: -below +above  [the nozzle]

Z clearance, 704-719
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
	#define Z_CLEARANCE_DEPLOY_PROBE   5 // Z Clearance for Deploy/Stow
	#define Z_CLEARANCE_BETWEEN_PROBES  5 // Z Clearance between probe point
	
Stepper directions, 750-765
---------------
		// Invert the stepper direction. Change (or reverse the motor connector) if an axis goes the wrong way.
	#define INVERT_X_DIR true
	#define INVERT_Y_DIR true
	#define INVERT_Z_DIR false

	// Enable this option for Toshiba stepper drivers
	//#define CONFIG_STEPPERS_TOSHIBA

	// @section extruder

	// For direct drive extruder v9 set to true, for geared extruder set to false.
	#define INVERT_E0_DIR true
	#define INVERT_E1_DIR false
	#define INVERT_E2_DIR false
	#define INVERT_E3_DIR false
	#define INVERT_E4_DIR false
	
Bed size and travel limits, 782-792
---------------

	// The size of the print bed
	#define X_BED_SIZE 200
	#define Y_BED_SIZE 192

	// Travel limits (mm) after homing, corresponding to endstop positions.
	#define X_MIN_POS 0
	#define Y_MIN_POS 0
	#define Z_MIN_POS 0
	#define X_MAX_POS X_BED_SIZE
	#define Y_MAX_POS Y_BED_SIZE
	#define Z_MAX_POS 185
	
Bed levelling, 839-876
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

Bed levelling options, 912-923
---------------

	  // Set the number of grid points per dimension.
	  #define GRID_MAX_POINTS_X 3
	  #define GRID_MAX_POINTS_Y GRID_MAX_POINTS_X

	  // Set the boundaries for probing (where the probe can reach).
	  #define LEFT_PROBE_BED_POSITION 10
	  #define RIGHT_PROBE_BED_POSITION 150
	  #define FRONT_PROBE_BED_POSITION 10
	  #define BACK_PROBE_BED_POSITION 190

	  // The Z probe minimum outer margin (to validate G29 parameters).
	  #define MIN_PROBE_EDGE 8

Move between bed corners, 1004-1005
---------------
	// Add a menu item to move between bed corners for manual bed adjustment
	#define LEVEL_BED_CORNERS

Z safe homing, 1025-1034
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

M500 and M501 commands, 1111-1118
---------------
	// The microcontroller can store settings in the EEPROM, e.g. max velocity...
	// M500 - stores parameters in EEPROM
	// M501 - reads parameters from EEPROM (if you need reset them after you changed them temporarily).
	// M502 - reverts to the default "factory settings".  You still need to store them in EEPROM afterwards if you want to.
	//
	#define EEPROM_SETTINGS // Enable for M500 and M501 commands

Preheating, 1147-1154
---------------
	// Preheat Constants
	#define PREHEAT_1_TEMP_HOTEND 180
	#define PREHEAT_1_TEMP_BED     70
	#define PREHEAT_1_FAN_SPEED     0 // Value from 0 to 255

	#define PREHEAT_2_TEMP_HOTEND 225
	#define PREHEAT_2_TEMP_BED    90
	#define PREHEAT_2_FAN_SPEED     0 // Value from 0 to 255

SD support, 1325-1332
---------------
	/**
	 * SD CARD
	 *
	 * SD Card support is disabled by default. If your controller has an SD slot,
	 * you must uncomment the following option or it won't work.
	 *
	 */
	#define SDSUPPORT

Feedback sound, 1405-1413
---------------
	//
	// The duration and frequency for the UI feedback sound.
	// Set these to 0 to disable audio feedback in the LCD menus.
	//
	// Note: Test audio output with the G-Code:
	//  M300 S<frequency Hz> P<duration ms>
	//
	#define LCD_FEEDBACK_FREQUENCY_DURATION_MS 0
	#define LCD_FEEDBACK_FREQUENCY_HZ 0

Smart controller, 1464-1470
---------------
	//
	// RepRapDiscount Smart Controller.
	// http://reprap.org/wiki/RepRapDiscount_Smart_Controller
	//
	// Note: Usually sold with a white PCB.
	//
	#define REPRAP_DISCOUNT_SMART_CONTROLLER


Marlin_main.cpp
===============

Line 13206
---------------
	        planner.buffer_line(delta[A_AXIS], delta[B_AXIS], raw[Z_AXIS], raw[E_AXIS], _feedrate_mm_s, active_extruder);
	        
	        
Version.h
===============


pins_GT2560_REV_A_PLUS.h
===============

Bltouch, 31-35
---------------
	#if ENABLED(BLTOUCH)
	  #define SERVO0_PIN  11
	#else
	  #define SERVO0_PIN  11
	#endif







