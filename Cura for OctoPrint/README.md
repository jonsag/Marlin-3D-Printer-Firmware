#Cura for OctoPrint

OctoPrint slicer uses Cura config files  
However, Cura must be version 15.04 or lower  

Download it here:  
https://ultimaker.com/en/products/ultimaker-cura-software/list  

Or use my configs on this page  

200-65, 0.2mm, 3perims, 40mmps, al
---------------
Extruder temp: 200 C  
Bed temp: 65 C  

Layer height: 0,2 mm  
Wall thickness: 1,2 mm  
Bottom thickness: 0,2 mm  

Support: none  
No of perimeters: 3  

Print speed: 40 mm/s  

Fill density: 30%  

Nozzle size: 0,3 mm  
Filament diameter: 1,75 mm  

Start code:  

	M280 P0 S160 ; BLTouch alarm release
	G4 P100 ; delay for BLTouch
	G28 ; home all axes
	G29 ; auto bed leveling
	G1 Z10 F5000 ; lift nozzle
	G92 E0 ; set extruder length to zero

End code:  

	M104 S0 ; turn off extruder heating
	M140 S0 ; turn off bed heating
	G28 X0  ; home X axis
	M84     ; disable motors

	