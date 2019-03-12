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

Min temps, 315-323
---------------
	// The minimal temperature defines the temperature below which the heater will not be enabled It is used
	// to check that the wiring to the thermistor is not broken.
	// Otherwise this would lead to the heater being powered on all the time.
	#define HEATER_0_MINTEMP 10
	#define HEATER_1_MINTEMP 5
	#define HEATER_2_MINTEMP 5
	#define HEATER_3_MINTEMP 5
	#define HEATER_4_MINTEMP 5
	#define BED_MINTEMP 10

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

Bed size and height, 782-792
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
	Bed levelling options, 912-920
	  // Set the number of grid points per dimension.
	  #define GRID_MAX_POINTS_X 3
	  #define GRID_MAX_POINTS_Y GRID_MAX_POINTS_X

	  // Set the boundaries for probing (where the probe can reach).
	  #define LEFT_PROBE_BED_POSITION 10
	  #define RIGHT_PROBE_BED_POSITION 150
	  #define FRONT_PROBE_BED_POSITION 10
	  #define BACK_PROBE_BED_POSITION 190




