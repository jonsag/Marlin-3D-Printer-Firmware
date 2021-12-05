# Arduino IDE

## Compiling and uploading on Arduino IDE

Download and install Arduino IDE 1.8.x from [https://www.arduino.cc/en/software](https://www.arduino.cc/en/software)  

Open Arduino IDE and open /path/to/Marlin.ini  

Select board:  
    Tools -> Board: ... -> Arduino AVR Boards -> Arduino 2560 or Mega 2560  

Select processor:  
    Tools -> Processor: ... -> ATmega2560 (Mega 2560)  

Set port:  
    Tools -> /dev/ttyUSB0 (or whatever...)  

Select programmer:  
    Tools -> Programmer: ... -> AVRISP  

Compile and upload!  

## Working with binary files

Instead of directly uploading the compiled code with Arduino IDE you can save the compiled code for later upload.  

### Export firmware to binary

Start Arduino IDE and select file and board as above.  

Click 'Sketch -> Export compiled binary'  

The IDE now compiles the firmware to a binary file in the same location as your Marlin.ini.  
It will be called Marlin.ino.mega.hex  

Move the file, and rename it to something sensible.  
