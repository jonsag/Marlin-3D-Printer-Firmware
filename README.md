# Marlin 3D Printer Firmware

Everything in this repo is for Geeetech I3 Pro B  

*************
Refer to .md file for the Marlin version you want to use.  

Read that file carefully, PLEASE!
*************

## Marlin firmware for my Geeetech i3 Pro B with GT2560A+ board  

Includes BLTouch, T8 lead screws and RepRap Discount Full Graphic Smart Controller.  

I recommend using VSCode for compiling and uploading to printer.  

## Compilation

I use [VS Code](https://code.visualstudio.com/) with [PlatformIO](https://platformio.org/) and [Auto Build Marlin](https://marlinfw.org/docs/basics/auto_build_marlin.html) for compiling, but you can also do this with [Arduino IDE](https://www.arduino.cc/en/software).  

VS Code/PlatformIO instructions [here](<./VSCode, Installation, Compiling and Uploading.md>).  

## Testing and calibrating

View current settings and parameters  
> M503

### BLTouch

#### Set Z offset

View current offset  
> M851 ; view current Z offset

    Send: M851
    Recv: echo:Probe Z Offset: -0.95
    Recv: ok

Heat up bed
> M140 S75 ; set bed temp to 75

Home all axis
> G28 ; home all axis
>
Disable software end stops  
> M211 S0 ; disable software end stops

Do the paper test and bring down Z slowly.  
Note the Z value.  
> M114 ; get current position

Set new offset  
> M851 Z-0.8

    Send: M851 Z-0.8
    Recv: echo:Probe Z Offset: -0.80
    Recv: ok

Save new value to EEPROM  
> M500

You can also adjust the Z offset during prints.  
Double click the knob and adjust the offset until it's OK.  
Then insert new value as above.  

Higher value -> smaller distance from bed  

#### Sensor test

> M280 P0 S10 ; pushes the pin down  
> M280 P0 S90 ; pulls the pin up  
> M280 P0 S120 ; self test – keeps going until you do pin up/down or release alarm  
> M280 P0 S160 ; release alarm  

### PID Tuning

Check current settings  
> M503 ; print all settings stored in eeprom  

    ...
    Recv: echo:; Hotend PID:
    Recv: echo:  M301 P23.12 I1.72 D77.65
    ...  

#### Hotend PID Tuning

Start parts cooler fan  
> M106 S255 ; set parts fan to 100%  

    Send: M106 S255
    Recv: ok

Start tuning  
> M303 E0 S245 C8 ; tune at 245 degrees 8 times  

    ...
    Recv: PID Autotune finished! Put the last Kp, Ki and Kd constants from below into Configuration.h
    Recv: #define DEFAULT_Kp 17.06
    Recv: #define DEFAULT_Ki 1.05
    Recv: #define DEFAULT_Kd 69.18
    ...

Enter new values  
> M301 P17.06 I1.05 D69.18 ; set hotend PID values  

    Send: M301 P17.06 I1.05 D69.18
    Recv: ok

Save to EEPROM  
> M500 ; store to eeprom  

    Send: M500
    Recv: echo:Settings Stored (627 bytes; crc 55228)
    Recv: ok

Stop parts cooler fan  
> M106 S0 ; turn off parts fan

#### Bed PID Tuning

Start tuning  
> M303 E-1 S75 C8 ; tune at 75 degrees 8 times

    ...
    Recv: #define DEFAULT_bedKp 49.22
    Recv: #define DEFAULT_bedKi 9.39
    Recv: #define DEFAULT_bedKd 172.04
    ...

Enter new values  
> M304 P49.22 I9.39 D172.04 ; set bed PID values  

    Recv: ok

Save to EEPROM  
> M500 ; store to eeprom

### Set temperatures

Set extruder temperature  
> M104 S205 ; set temp for default extruder to 205 degrees  

    Send: M104 S205
    Recv: ok

Set bed temperature  
> M140 S65 ; set bed temp to 65 degrees

    Send: M140 S65
    Recv: ok
    ...

### Steps/mm

Show current settings (steps per mm etc)  
> M501

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

### Set X/Y center

Home X and Y axes  
> G28 X Y

Set extruder at 0:0  
> G1 X0 Y0

Set extruder at bed center  
> G1 X95 Y96

if bed size is set to 190x192mm in Configuration.h in Marlin firmware  

    // The size of the print bed
    #define X_BED_SIZE 190
    #define Y_BED_SIZE 192

Compensate with  

    #define X_MIN_POS 0
    #define Y_MIN_POS 0
    ...
    #define X_MAX_POS X_BED_SIZE
    #define Y_MAX_POS Y_BED_SIZE

### Homing and leveling

> G28 ; home all axes
> G29 ; do bed leveling

### Set skew factor

Adapted from [https://github.com/MarlinFirmware/Configurations/blob/import-2.0.x/config/examples/Geeetech/Prusa%20i3%20Pro%20B/bltouch/README.md](https://github.com/MarlinFirmware/Configurations/blob/import-2.0.x/config/examples/Geeetech/Prusa%20i3%20Pro%20B/bltouch/README.md)  

The skew factor must be adjusted for each printer:  

First, uncomment `#define XY_SKEW_FACTOR 0.0`, if commented  

      #define XY_SKEW_FACTOR 0.0

Compile and upload the firmware.  
Then, print [YACS (Yet Another Calibration Square)](https://www.thingiverse.com/thing:2563185).  
Hint: scale it considering a margin for brim (if used). The larger, the better to make error measurements.  
Measure the printed part according to the comments in the example configuration file, and set `XY_DIAG_AC`, `XY_DIAG_BD` and `Y_SIDE_AD`.  

      #define XY_DIAG_AC 282.8427124746
      #define XY_DIAG_BD 282.8427124746
      #define XY_SIDE_AD 200
  
Comment `#define XY_SKEW_FACTOR 0.0` again.  

      //#define XY_SKEW_FACTOR 0.0

Compile and upload again.  

## Permissions

Check your permissions.  
You need to belong to the groups tty and dialout to be able to write to the tty/USBx.  

Run  
>$ groups | grep ' tty ' && echo -e "\nGreat! \nYou are a member of 'tty'" || echo -e "\nError: \nYou are not a member of the group 'tty'. \n\nCorrect with 'sudo usermod -a -G tty $USER'"

and  
>$ groups | grep ' dialout ' && echo -e "\nGreat! \nYou are a member of 'dialout'" || echo -e "\nError: \nYou are not a member of the group 'dialout'. \n\nCorrect with 'sudo usermod -a -G dialout $USER'"

to check.  

If you had to add yourself to any group, you must reboot to join the groups.  

>$ sudo reboot

## avrdude

Install avrdude if not installed.  
>$ sudo apt install avrdude

### Upload binary

>$ avrdude -v -q -p m2560 -c wiring -P /dev/ttyUSB0 -D -U flash:w:/path/to/image.hex:i
