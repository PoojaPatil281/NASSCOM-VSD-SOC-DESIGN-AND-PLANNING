# NASSCOM-VSD-SOC-DESIGN-AND-PLANNING
 Hello, everyone! I'll be sharing what I have learned during a 5-day workshop on VLSI SOC design and planning using openLANE tool and sky-130nm under the guidance of Director and Co-founder of 	VLSI System Design(VSD) pvt.ltd, Kunal Ghosh

## Day 1 : Inception of open-source,openLane ans sky130 PDK
Chip has ollowing parameters

- Pads : It is used to send signal from inside and outside the chip.
- Core : It is the place where logical gates and connections  are present.
- Die : It is the place where chip is present.
  
 ![chip](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/08532765-45fd-46ae-8fc1-6acb0486cd8a)

### RTL to GDS Flow
- Synthesis : It is the process of converting RTL into technology dependent gate level netlist.
- Floorplanning and Power planning : In Floorplanning we decide the placement of macros,IO’s,core width and height. In powerplanning we decide power ground structure and ensures that uniform power is distributed all over the chip.
- Placement : In this step, placement of standard cell is done and ensures that if it is properly placed in standard cell rows.
- CTS : In clock tree synthesis, clock tree structure is defined which has minimal skew.
- Routing : In this step, physical connection of metal layers are done for all logical connection present in the design.
- Signoff : In this step, we decide if design follows DRC rules and meets timing requirement.

![rtl to gds](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/08e04d23-806d-4390-b3fd-268d504fc610)

### openlane ASIC flow
![openlane flow](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/bfeab34c-b68e-4f77-b1a3-10eb720a0fd9)

Tool used here is openLANE. It is basically of flow.
the main aim of openLANE is to have complete RTL to GDS flow. so you put RTL and what u have at the end is GDSII file. This tool is very similar to commercial EDA tool.
Whenever you want to know more about commands in linux use commandd : eg : ls –help

### Openlane directory structure 
PDK we are using here is sky130A.
![a](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/1a5c0920-736e-4592-befa-0152910a98b2)
here skywater-pdk folder contains information related to timing,cell lef,technology lef. skywater-pdk files are silicon foundry related files. This files are made to work with commercial EDA tools and not for opensource EDA tools.so open_pdks folder added here to mitigate this problem. basically they are sets of scripts and files that converts this foundry level PDK’s to be compatible with open source EDA tools like magic(for layout),netgen.
Sky130A folder is that folder which has been made comfortable to work with opensource environment.
![b](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/563968d4-8e62-4160-bce1-a6174e1cc9c2)
libs.ref folder contains file related to cell lef,timing that is specific to technology.
libs.tech folder contains file related to tool that is specific to tool.
![c](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/7b1562d3-46a1-4a62-8319-ad5a041165c7)
Here klayout,magic,qrflow,openlane,ngspice are the tools.We would be working on pdk variant- sky130_fd_sc_hd.Here sky130 is process name..130nm…fd is abbreviated foundry name. so fd is skywater foundry name. sc is standard cell library. hd is a pdk variant and hd stands for high density.
![d](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/e7ac9164-a843-4a13-bb37-90ec47f97029)
So tech lef file contains the metal layer information.lib file contains timing files.
![e](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/040ce9d4-7ace-4445-a16d-070b96687720)
![f](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/6407fd5e-2aa3-4831-ae1b-b856d9b1fff2)
![g](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/837c2314-7f2d-4a47-a1c5-8c0ecca759b5)
Inside openlane folder :
![h](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/44472f4d-f197-4a46-9d2a-eae94ac2ac8b)
Inside design folder :-there are 30-40 design but here we are using design picorv32a.
![i](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/4d62f7b1-9708-4b37-a7d7-88a7501d32f0)
Inside picorv32a design:
![j](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/a597a6a4-9135-4f0c-862b-1e11ced4eb3c)
src folder contains RTL and SDC file.
![k](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/fd5880c5-4b8e-465e-ae24-12e053dbdbbe)
openlane have default switches so everytime you have to create your own config.tcl file that contains info about clock period,design name,clockport,Verilog file path,sdc file path so this config.tcl file will overwrite the default setting present in openlane. 
![l](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/a1fc2019-539c-4b08-a7cd-65785510bd58)
![m](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/b51e5285-7143-47c8-bb4c-ffe9d20eace5)
This file is also another same kind of config.tcl file. Which is the highest priority file so whatever the content present in config.tcl file will get overwrite by this file. So in conclusion, first it take default switches present in openlane then config.tcl will overwrite those switches, again if sky130A_sky130_fd_sc_hd_config.tcl file present then it will overwrite the content of config.tcl file.To open file use cmd :- less filename.tcl

### Tool Invoking, Extracting packages and data preparation steps
- Tool Invoking
Command used for invoking tool is docker.After invoking tool, before performing synthesis,first step is data preparation.
![n](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/affd302a-0d26-4d38-ba55-68c19b9bbdd4)
here interactive meaning is running in step by step.
- Package Extraction
Command used : package require openlane 0.9
- Date Preparation
Command used : prep -design picorv32a
data preparation merge both cell lef & tech lef into one file.so after data preparation you can see that there is a formation of runs directory.








