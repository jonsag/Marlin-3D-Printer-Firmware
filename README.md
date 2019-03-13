# Marlin 3D Printer Firmware

Everything in this repo is for Geeetech I3 Pro B  

Marlin firmware for my Geeetech i3 Pro B with GT2560A+ board  
===============
Includes BLTouch and T8 lead screws  

When compiling and uploading with Arduino IDE:  
Set board:  
Tools > Board > Arduino Mega 2560  
Also set correct port, ie /dev/tty/USB0  

Testing and calibrating
===============

BLTouch
---------------
M280 P0 S10 ; pushes the pin down  
M280 P0 S90 ; pulls the pin up  
M280 P0 S120 ; Self test – keeps going until you do pin up/down or release alarm  
M280 P0 S160 ; Release alarm  

PID Tuning
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

Steps/mm
---------------
Show current settings (steps per mm etc)  
>M501

Returns  

	echo:V47 stored settings retrieved (614 bytes; crc 29566)
	echo:  G21    ; Units in mm
	echo:  M149 C ; Units in Celsius

	echo:Filament settings: Disabled
	echo:  M200 D1.75
	echo:  M200 D0
	echo:Steps per unit:
	echo:  M92 X81.50 Y81.50 Z400.69 E94.00
	echo:Maximum feedrates (units/s):
	echo:  M203 X400.00 Y400.00 Z2.00 E45.00
	echo:Maximum Acceleration (units/s2):
	echo:  M201 X4000 Y4000 Z40 E4000
	echo:Acceleration (units/s2): P<print_accel> R<retract_accel> T<travel_accel>
	echo:  M204 P3000.00 R3000.00 T3000.00
	echo:Advanced: S<min_feedrate> T<min_travel_feedrate> B<min_segment_time_us> X<max_xy_jerk> Z<max_z_jerk> E<max_e_jerk>
	echo:  M205 S0.00 T0.00 B20000 X10.00 Y10.00 Z0.30 E5.00
	echo:Home offset:
	echo:  M206 X0.00 Y0.00 Z0.00
	echo:Auto Bed Leveling:
	echo:  M420 S0
	echo:Material heatup parameters:
	echo:  M145 S0 H180 B70 F0
	echo:  M145 S1 H215 B105 F0
	echo:PID settings:
	echo:  M301 P22.06 I1.06 D114.78
	echo:Z-Probe Offset (mm):
	echo:  M851 Z-0.61
	
Set Z-Offset
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

Higher value -> larger distance from bed  
The above example will increase the distance from the bed, ie. the gap between nozzle and bed will be larger.  

Set X/Y center
---------------
Home X and Y axes  
>G28 X Y

Set extruder at 0:0  
>G1 X0 Y0

Set extruder at bed center  
>G1 X95 Y96

if bed size is set to 190x192mm at lines 782-792 in Configuration.h in Marlin firmware  

	// The size of the print bed
	#define X_BED_SIZE190
	#define Y_BED_SIZE 192
	
Compensate with  

	#define X_MIN_POS 0
	#define Y_MIN_POS 0
	...
	#define X_MAX_POS X_BED_SIZE
	#define Y_MAX_POS Y_BED_SIZE
	
	