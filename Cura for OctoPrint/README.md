#Cura for OctoPrint

OctoPrint slicer uses Cura config files  
However, Cura must be version 15.04 or lower  

Download it here:  
https://ultimaker.com/en/products/ultimaker-cura-software/list  

Or use my configs on this page  

200-65, 0.2mm, 3perims, 40mmps, al
---------------
Extruder temp, C  

	print_temperature = 200
	
Bed temp, C  

	print_bed_temperature = 65

Layer height, mm  

	layer_height = 0.2
	
Wall thickness, mm  

	wall_thickness = 1.2

Support  

	support = None
	
Adhesion:  

	platform_adhesion = None

Print speed, mm/s  

	print_speed = 40

Fill density, %  

	fill_density = 30

Nozzle size, mm  

	nozzle_size = 0.3
	
Filament diameter, mm  

	filament_diameter = 1.75

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

	