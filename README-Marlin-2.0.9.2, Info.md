# Firmware Marlin-2.0.9.2 for Geeetech I3 Pro B

Please scroll through whole document so you don't miss anything. :-)  

Instructions below are run on a Linux system.  

## Important note - MUST READ

There is a line you HAVE to change in configuration.h before compiling this.  

Uncomment line 1805 to disable my skew correction values.  

    #define XY_SKEW_FACTOR 0.0

Comment these out again after you've made the test print and measurements. Read more below.  

(It's not really a disaster if you forget this, but you will get a more skewed print probably.)  

## Other changes for different setups

Below are changes you have to do, if you have a different setup than I have.  

### IF you DON'T have a BLTouch or clone

Comment out line 1095  

    //#define BLTOUCH

### IF you DON'T have T8 lead screws

Comment out line 930  

    //#define PRO_B_WITH_LEADSCREW

### IF you have the STOCK LCD screen

Comment out line 2376  

    //#define REPRAP_DISCOUNT_FULL_GRAPHIC_SMART_CONTROLLER

and uncomment line 2218  

    #define REPRAP_DISCOUNT_SMART_CONTROLLER

### If you have a BLTouch or clone, not mounted in the same way I have

Check your probe offsets on line 1190  

    #define NOZZLE_TO_PROBE_OFFSET { xx, yy, -zz }

Check offsets on lines 1195-  

    #define PROBING_MARGIN_LEFT xx
    #define PROBING_MARGIN_RIGHT xx
    #define PROBING_MARGIN_FRONT yy
    #define PROBING_MARGIN_BACK yy

Check values on line 1694 for the "Level Corners" option  

      #define LEVEL_CORNERS_INSET_LFRB { xx, yy, xx, yy } // (mm) Left, Front, Right, Back insets

## Compilation

I use [VS Code](https://code.visualstudio.com/) with [Auto Build Marlin](https://marlinfw.org/docs/basics/auto_build_marlin.html) for compiling, but you can also do this with [Arduino IDE](https://www.arduino.cc/en/software).  

## Misc g-code

### Settings

>M503 ; view current settings and parameters
>M500 ; store settings to EEPROM
>M502 ; load settings from EEPROM

### BLTouch

>M280 P0 S10 ; pushes the pin down  
>M280 P0 S90 ; pulls the pin up  
>M280 P0 S120 ; Self test – keeps going until you do pin up/down or release alarm  
>M280 P0 S160 ; Release alarm  

### Homing and leveling

>G28 ; home all axes
>G29 ; do bed leveling
