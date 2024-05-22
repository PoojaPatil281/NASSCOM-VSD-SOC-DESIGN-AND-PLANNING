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
Command used for invoking tool is docker.After invoking tool, before performing synthesis,first step is data preparation.
![n](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/affd302a-0d26-4d38-ba55-68c19b9bbdd4)

here interactive meaning is running in step by step.
- Package Extraction
Command used : package require openlane 0.9
- Date Preparation
Command used : prep -design picorv32a
data preparation merge both cell lef & tech lef into one file.so after data preparation you can see that there is a formation of runs directory.

## Synthesis 
Command used :  run_synthesis .
![o](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/34c19cea-b57b-499f-b7a7-d8335357b66d)
Calculation of Flop Ratio and DFF % from synthesis statistics report file.
Flop ratio = No. of Flipflop/No. of Cells
                  =1613/14876
                   =0.1084
DFF % = 0.1084 * 100 = 10.84%

# Day 2 : Good Floorplan vs Bad Floorplan and Introduction to library Cells
Define width and Height of core die.
![p](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/91e5fd88-dfda-4da5-81d9-b1fc24c6d224)
Lets consider an example 1 of Netlist shown below
![q](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/f7c9e019-7060-4372-bdcd-93e920cba3bd)
Netlist basically defines connectivity between all the Elements.Dimension of chip is mostly depends on dimension of the logic gates.Lets consider the dimension standard cell as 1unit X 1unit.so the area of each standard cell will become 1sq.unit.And also assumes same area for Flipflop as shown below.
![r](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/e7cdd758-f030-41f6-9c6a-296216ae016d)
so the minimum area Occupied by the netlist is: 2unit X 2unit.
Utilization Factor : It is the area occupied by netlist to the total area of the core. When Utilization factor is 1 that is 100% which means core is completely occupied by the logic.
Aspect Ratio : Height of core to the width of core. When aspect ratio is 1 it indicates that the chip is square shape. when aspect ratio is other than 1,itindicates that the chip is rectangular shape. 
![s](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/96481d09-71e6-4144-9b6d-39d7c250047a)
![s](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/d337e570-f95a-43f8-a847-ebe6ed58c65e)
Example 2 : Consider a square shape chip and the dimensions of core height is 4 unit and width is 4 unit. And also Consider logic is also placed inside the core as shown below.
![t](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/50122d11-7301-444f-9ab8-a381c481790a)
Utilization = 2 unit x 2 unit / 4 unit x 4 unit=0.25
It says that out of complete chip area 25 % of area is occupied by the logic and the remaining 75% of area is available for optimization and routing.
Aspect ratio = 4 Unit /4 Unit =1
It says that the chip is square shape.
Define Location of Preplaced Cells : 
Preplaced cells are the IP’s such as memory,clock gating cell, comparator, mux. All of them can be implemented once and can be instantiated multiple times on to a netlist. This IP’s are the part of top level netlist so they receives input and delivers output signal but the functionality of this cells should be Implemented once. Hence they are called as Preplaced cells.these cells are placed only once in the chip.the arrangement of these IP’s in a chip is referred as Flooplannning.this arrangement should be perform before routing.since they are placed before actual placemnt and routing hence they are called as Preplaced cells.
![u](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/d6ec098b-92f1-433d-870d-c1230d5ff49c)
Surround pre-placed cells with Decoupling Capacitors :
Decap cells are placed across the Memories or blocks that will supply the required amount of charge to this block whenever they are switching that is current demand of each block or macros is handled by decap cells. Basically, it ensures that there should not be any crosstalk issue.
![v](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/80f9e3f6-ee78-41c8-b34c-c57ba3ffdb83)
Power Planning : 
Instead of single power supply, multiple power supply can also be built throughout the chip to ensure that uniform power should be deliver throughout the chip. So any logic present in the design will take power from its nearer power supply or it will drop a current to its nearer ground. This is basically called as Power mesh. 
![w](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/d94c3ede-8985-4d86-ab53-032400635fa5)
Pin Placement :
Clock ports is bigger in size than data ports since clock ports contineously sends signals to flipflop so for that it needs least resistance path. 
![x](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/933c2b5a-edb4-4fb3-8c06-84530a671a35)
Logical Cell Placement Blockage : This Blockage ensures that there should not be placemnet of cells in between core and die. 
![y](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/bbe1a6a0-6749-4aa7-abbf-6125a054253d)
### Floorplan Lab 
To run floorplan command used is run_floorplan.
Screenshots of floorplan run
![z](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/4bd3f50c-6431-4aa4-9b28-8909e7a00daa)
![a](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/c49b0f84-dd62-451e-a35e-8b46133dc199)
Default parameters that are set for floorplan stage in openlane.(path:Desktop/work/tools/openlane_working_dir/openlane/configuration/floorplan.tcl)
![b](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/8c24e50e-a2c5-45a3-852a-0b80a9258871)
FP IO mode is basically how we want pin configuration around the core.FP IO mode = 1 means pin possition is random but at equidistance.FP IO mode = 0 means pin possition will not be equidistance.Here default core utilization is 50%,FP IO VMETAL as 2 and FP IO HMETAL as 3. In openlane flow vertial metal layer and Horizontal metal is one more than what is specified. So VMETAL will be 3 and HMETAL will be 4. sky130A_sky130_fd_sc_hd_config.tcl this file will overwrite the default setting present in openlane.
![c](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/8b110530-9eb5-44d1-af20-84578eeae803)
Hence utilization = 35%
![d](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/3b33fb54-fc5b-4aa6-baa6-33064e577d93)
Layout of Floorplan in Magic
![e](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/ade64281-463d-4c9c-9e4e-35b91a5043ac)
![f](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/a5b826e3-9be1-4f8d-ad42-ca4c5fca72d6)
To highlight object press s,press v to fit it on screen.
Equidistance placement of ports 
![g](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/84dc73dd-44c4-4e31-92df-83b819f20c04)
horizontal Ports layer set in config.tcl :- metal 3
![h](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/f738a769-484f-45b4-9749-2c5c2e781fae)
Vertical ports layer set in config.tcl : metal 4
![i](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/26e6638c-b560-4839-b18d-dc8cbcb2859a)
Placement of Decap cells and Tap cells 
![j](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/6fafdd0c-aaa0-46e0-ac03-524b0d2aa4b6)
Diagonally equidistance tap cells
![k](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/4e1785da-e88b-4d55-8524-89d9d4722d17)
Unplaced standard cells at origin
![l](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/15c181de-3938-4a1a-b8a5-0b7f1a0dd418)
### Placement 
Placement stages :
- Global Placement
- Detail Placement
Global placement aim is to reduce wirelength. In  openlane there is a concept of HPWL.HPWL stands for half parameter wire length.
Screenshots of Placement run 
![m](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/4c6293c2-3030-45fb-bddd-df715483247d)
![n](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/09fd25ae-c641-4445-b115-6871ab026b4d)
Number of instances ,fixed instances, utilization
![o](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/8cfdba44-a40c-4419-a866-3cdda0281551)
placement def in Magic
![p](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/dca7bacf-4756-4759-ac7a-9a6ca3ad97cc)
Standard cells placed legally in standard cells rows
![q](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/4640850c-3d8a-4171-8814-9db93ec0ed2d)
In openlane power planning is performed after CTS stage.


# Day 3 :  Design library cell using Magic layout and ngspice characterization
Performing SPICE extraction and post layout spice simulation of Inverter we have done Clonning of vsdstdcelldesign directory from github link in openlane directory.![r](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/01071da2-a06e-41d1-a3f0-0321b5d0e541)
Now you can see the directory vsdstdcelldesign inside openlane as shown below
![s](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/a6f271a0-7bb4-4c74-ab09-a2c590333076)
Copy magic tech file i.e.sky130A.tech file inside vsdstdcelldesign directory
![t](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/2aef5dce-0d88-4d07-9f09-89d6e3d4f32b)
Now open sky130_inv.mag file in magic tool 
![u](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/8c4cd260-ffdc-4551-bb5c-2e126510d692)
Inverter layout in magic:-
![v](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/fac889ec-49c1-43b9-bf14-99895c0a4e8c)
nmos : when polysilicon crosses n diffusion then it is a nmos.
![w](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/f7c2ecbf-ae9d-404f-b95e-47fcf32f87b6)
pmos : when polysilicon crosses p diffusion then it is a pmos.
![x](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/0cf1431c-0fc7-46f3-8147-84ce507e0d46)
To check connectivity,press s 3 times
Example 1 : check connectivity of pmos drain and nmos drain, selected area shows connectivity as shown below
![y](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/de4bd27c-c79c-43a6-9aa3-290f6548a0ae)
Example 2 : Connectivity of pmos and vdd (press s 2 times)
![z](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/6e3a5426-45dc-4158-bb53-d4cca8710b2b)
Example 3 : nmos and vss connectivity(press s 2 times)
![a](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/38c4fb62-50e9-4b8c-904e-e9fa41267ec9)

### Lab Steps to create standard cell layout and extract spice netlist
Extract the spice netlist from the inverter using Magic tool. 
![b](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/9894dfa9-c82a-40f1-9c8a-97124265684c)
![c](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/d29e1066-b691-4e8b-9622-0f555c0d9d90)
After that use command ext2spice,this will create a spice file which is basically a extracting parasitic capacitance in the vsdstdcelldesign directory.
![d](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/c5e04522-974f-441f-a62e-53e993a76f15)

### Lab steps to create final SPICE deck using Sky130tech 
After Extracting SPICE file we need to update it according to the design.
![e](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/3699301f-9a9b-438b-bb6c-589a07246e10)
![f](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/fd23d586-a5a4-4165-b9a1-0fd620cb688d)
Now the next step is to run the SPICE file in  ngspice tool by using command ngspice sky130_inv.spice
![g](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/241e12ef-892a-4719-ba5b-1d1a67ef41f0)
Now we need to check output vs time i.e transient response for that use command plot y vs time a
![h](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/6bd219f7-89e4-499d-ad78-f07dd9c7825d)

### Lab steps to characterize inverter using sky130 model files
Characterizing a cell means to find out 4 parameters such as:
- rise transition : Time taken for output waveform to transit from a value of 20% of a maximum value to 80% of maximum value.
- Fall time : Time take to fall output from 80% to 20%
- Propagation time
- Cell fall delay
Rise time : 
Plot of output vs input time a
here maximum value is 3.3v so 20% of 3.3 is 0.66
![i](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/95dcb717-e7af-410d-b07a-ddbdc26ea9cf
So Rise time = 2.244-2.181=0.063ns
Fall time :
![j](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/9e440ecd-59bb-4b4c-af87-9467499b647f)
Fall time = 4.095-4.051=0.044ns
Cell rise delay : It is the time taken for the 50% of transition from 0 to 1 at the output for the 50% transistion from 1 to 0 at the input side.
![k](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/796b0a95-7c95-46a4-be39-6ed308c9bf17)
Cell rise delay = 2.21-2.15= 0.06ns
Cell Fall delay : It is the time taken for the 50% of transition from 1 to 0 at the output for the 50% transistion from 0 to 1 at the input side.
![l](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/527a6934-0913-4bec-b5c9-c6de27aa67d2)
Cell fall delay = 4.076-4.049=0.027ns
This is how characterization of cell is done at room temperature 27 degree celcius, normal temperature = 27 degree celcius, voltage = 3.3v

Now next objective is to use layout of this inverter and create a lef file and that lef file we will be using in openlane and will make a custom cell & also gives a custom name to that cell and will use this cell into picorv32a core and checks whether if openlane takes this cell or not and we will see what are the challenges we have to face.

### Lab Intoduction to Sky130 pdk’s and steps to download labs
Download the lab files in the home directory using command : tar xfz drc_test.tgz
![m](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/1153b67d-e0d5-4cb3-9476-69a0b90be5ff)
Wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
Now to extract the labs from downloaded zip file use command : tar xfz drc_test.tgz
In the downloaded files,there is a file called .magicrc that file serves as the start-up script for MAGIC.
![n](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/cbd9db28-4d6e-4760-9ad7-4a6f673caf13)
.magicrc file
![o](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/c879e11e-8cba-430d-a6b5-3eebd328540b)

### Lab Introduction to Magic and steps to load Sky130 tech-rules
To open the magic tool use command : magic -d XR 
![p](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/f5adfae1-1881-4ca4-a88c-d9cb4d2d3389)
set of rules for metal 3: For that load file metal3.mag
![q](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/1e044c5e-6b55-4136-80bc-a7ccf5cee1ab)
![r](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/33468812-37bd-4ad8-a89d-0430a3a4a84f)
Here m3.1, m3.2, m3.5, m3.6 are the independent example layout geometries and most of them shows some kind of drc’s error.
M3.6 shows minimum area drc,m3.5 shows via overlapping, m3.2 shows metal spacing,m3.1 shows metal width drc as shown below
![s](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/0b187297-2239-4998-9fb3-6ebe2fd390e2)
Now select an area in gui and fill the selected area with metal 3 by clicking on metal3 option. Then type a command cif see VIA2 so that area which was initially filled with metal 3 get filled with VIA2  mask as shown below.
![t](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/22f84014-4642-4c9d-82d6-342037eb71c3)

### Lab exercise to fix poly.p error in Sky130 tech file
Load poly file using command:- load poly
Use what command to check name of selected mask layer
![u](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/9ffecdef-cda4-4515-8d39-6fc1e5f0c338)
![v](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/77e7b549-8e4f-46b1-bb54-5459e7272462)
use box command to get width and height of selected box
![w](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/5fb4a9d2-070a-4265-8238-992cc9bd38f3)
![x](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/966b9a98-0472-4adc-b00f-24c5a5afaaec)
check the spacing between poly resistor and poly and compare this value with actual value in Skywater website. It can be clearly observe that there is a spacing error.Lets fix this spacing error.
Now make changes in Sky130a.tech file as shown below.
Before :
![y](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/adc1921b-57df-46f4-9585-705bbebfb50a)
After :
![z](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/2c3479c2-80fb-4010-9ccc-f03071d8638f)
Before :
![a](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/680b044d-7729-491a-9717-9d42ae0eb66f)
After:
![b](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/e53d27ef-a7d8-4a4c-a4e7-055daaab7f9f)
Now after updating tech file load it again and check for errors using command drc check.
Screenshots of fixed spacing drc issue between polyresistor and poly.
![c](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/d6d29053-2999-4a0d-9923-7c068448c6da)


# Day 4 : Pre-layout timing analysis and importance of good clock tree
### Lab steps to convert grid info to tract info 
we previously opened mag file using command – magic -T Sky130A.tech Sky130_inv.mag
Mag file contains info about power ground,port,logic path information but for PNR the only information you need is information about core boundry,power gnd rails,input and output port.so LEF file have all this information. So next objective is to extract a LEF file from mag file and then check whether we can plug that extracted file into picorv32.
To make standard cell we need follow some guidelines such as :
- The input and output port must lie on the intersection of vertical and horizontal tracks.
- The width of standard cell should be in odd multiple of track pitch and height should be in odd multiple of track vertical pitch.
![d](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/9a09f28e-c425-4b98-ad29-a43aac0b7c53)
open track file
![e](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/73b7be42-30e8-42ee-857f-6e81b0a19b98)
![f](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/9ab9ef29-7daf-41c9-8a61-fb01e3595c45)
Here li1 X Y 0.23 0.46 :---- 0.23 is horizontal track pitch offset,0.46 is horizontal pitch
li1 X Y 0.17 0.34 :----- 0.17 is vertical tack pich offset, 0.34 is vertical pitch
X & Y are the metal layer direction.
converge grid with tack value to check whether input port X and output port Y are on the intersection of vertical and horizontal of li1 layer. Since input and output port are defined on li1 layer.
grid before : press g
![g](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/2e9d2e17-a822-4791-95a3-a89669a6710a)
grid after :
![h](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/e1584fbc-9b61-49ad-8cf4-cdee5e3945d8)
So here we converged grid defination into a track defination and routing of li1 layer will happen on this layer.
Intersection of horizontal and vertical track are on the input and output port as shown below
![i](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/73b09409-980f-478c-aa82-4c4203b89e57)
This ensures that route can reach on this port from x and y direction.

### Lab steps to convert magic layout to std cell LEF
Save above mag file as sky130_vsdinv.mag
Extracting lef file :
![j](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/cdc5f39a-70da-44a1-ab9b-a8f674e0c64d)
![k](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/3d605293-60e5-416d-9851-0a3313aa4dc0)
![l](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/c9456f40-2db8-4884-b54c-393837877897)
Now we will plug this lef file into picorc32a,copy LEF file into src directory which is inside picorv32a.
![m](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/33d514f1-44b0-4d98-a322-d4630e7f5d5e)
To map vsd cell during synthesis,library file is required.so copy libs which is in libs which is inside vsdcelldesign directory.
![n](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/0ed99c9d-06ce-45ed-b686-7e5e48867e8e)
Modified config.tcl file which is inside picorv32a directory.
![o](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/e8487894-8087-4bec-bc93-01f80548f241)
LIB_MIN,LIB_MAX,LIB_TYPICAL is used for STA analysis.
LIB_SYNTH is a abc mapping file.
![p](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/dfcb259e-cf07-4076-b8cc-e18cda524f78)
invoke a tool 
![q](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/9989154e-f6c8-42e7-912f-d3dd5070ce8b)
run_synthesis 
![r](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/239c1586-bb32-4426-bf80-2d6df1db15fc)
Wns is maximum slack
Chip area:
![s](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/3407f4da-5748-4f98-b9d7-b1a6abd0e711)
Minimum slack or hold slack : 
![t](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/3e5120e5-7243-491a-8636-5184c931654a)
Fixing setup slack i.e max slack
We will balance delay and area by using a strategy.first we will check what is the strategy that have set in design.
![u](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/ec5720c6-5e5a-469c-bb34-c605d21fd92a)
![v](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/18cde149-fab0-45f7-9139-04f44428bf1a)
We will set SYNTH_BUFFERING and SYNTH_SIZING to 1

Buffering :- inserting a buffer to reduce wire delay.example : reset pin goes everywhere in chip so we want those high fanout nets to be buffered in order to reduce delay.
![w](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/f154c443-fa2c-43df-9137-a2fd86abfbb6)

Driving cell :-The cell that drive input ports.If input port has lots of fanout then high drive strength cell is needed to drive input port.
Now once again we will run synthesis to check whether setup slack is reduced or not
run_synthesis
![x](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/f282c8b9-8e89-47f5-a576-341e8a85c26f)
![y](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/24aa49d6-552b-4e73-9015-ca716d0c458d)
WNS & TNS =0
Chip area:
![z](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/5c12a032-622c-4443-b1be-f0ed6207e38c)
Before : WNS = -22.17 & TNS =-639.39
chip area =147712.918400
After: WNS & TNS =0ns & chip area= 181730.54400
can observe the custom vsd Inverter cell
![a](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/5d7d5440-ee4f-400c-bf03-95f911292ef1)
Can also check whether custom vsd invgerter cell is present in merged.lef file
![b](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/34ecf86d-fac7-4c65-bfce-6e3abe77bc56)
run_floorplan
Issues I faced due to failed flow that I had to manually run the flow.
![c](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/304bb2d7-981b-489f-b768-0c530073cc41)
init_floorplan
![d](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/50fff443-327a-4cde-8930-3368cf24d471)
Place_io
![e](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/8d8d2c30-7d92-4469-8ffe-0baf565fa3f6)
Tap_decap_or
![f](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/5320f1e1-5fd6-4ad1-b1d8-a3bcb5480e63)
Run_placement
![g](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/6d4879d6-c362-4425-a8bf-15c1069251d7)
![h](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/b7007bd5-d433-43a8-a0df-f7f33573f812)
Placement Layout
![i](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/1df7e2cc-884a-468b-8c77-3afdd201f5f5)
![j](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/178dd62f-0620-48cf-bbb6-561e759c5e2c)
Can see the placement of custom vsd inverter cell
![k](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/090b242d-6e2c-48c5-ab8a-c1d55cf3a0cd)
![l](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/ed8b5202-6f77-4ea1-be29-ed273ef4a736)
![m](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/7a40cd01-520b-497e-bcee-350b8760ac82)
Can observe that metal1 layer which is taken from library is correctly align with metal 1 layer of custom inverter cell.

### Lab steps to configure openSTA for post-synthesis timing analysis
After Placement stage,create file pre_sta.confi file inside openlane directory
![n](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/87c96cd8-ccbe-4eb3-9f42-f3edde508131)
create file my_base.sdc file inside src directory of picorv32a
![o](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/d54ca8ae-23b6-4421-9181-89b696139b90)
to run pre_sta.conf in sta use command : sta pre_sta.conf
![p](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/3634ddd4-3f6b-43b9-b103-b82ecdd01cd8)
Setup slack : -5.59 (violated)
Fixing setup slack 
![q](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/1b7f5d9b-a9c5-4ad2-8060-53320973db11)
After Placement stage during pre sta analysis ,you can observe that input transition is high due to high output capacitance so we can optimize fanout value in openlane flow.
![r](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/976990b4-2a59-4a9b-b0da-e78f72e02253)
![s](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/6f5eed9e-63e3-4a18-a37f-f447494ec511)
Yon can see driver pin of net _13292_ and it is driving input pins of 2 loads
![t](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/b4b3849b-1aee-4a72-9cdd-2a07f8afe175)

### Clock Tree Synthesis
Default parameters that are set in CTS are :
![u](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/050d9f78-8f85-448b-b8ab-f94acce23145)
Here target skew is basically a global skew that is set to 200ps.ROOT_BUFFER need high driving strength.
![v](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/ff5edfdf-87b0-45c4-8cd7-e2e2d3fb712f)
CLOCK_TREE_SYNTH enables CTS and tirtonCTS is the tool which performs CTS. Here we are doing analysis for typical corner but not for multi corner. Since one of the drawback of tritonCTS is it cannot do optimization for multiple corner.
CTS_TOLERANCE defines the tradoff between QoR and Runtime. QoR stands for Quality of results.
Different QoR of CTS are:
- 	Better skew value
- 	50 % duty cycle	
Higher value of QoR means design is meeting the required specification but it will require longer runtime.
So higher value of CTS_TOLERANCE means lower runtime but worst QoR.
run_cts
![w](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/8380f13d-5ff2-4119-bf4b-0acd8b265ade)
In CTS stage buffers are added. So inside synthesis result directory you can observe the modified netlist file that contents previous netlist data and buffers that are added during CTS stage as shown below.
![x](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/2389b5b6-0e29-44ea-b21d-db00f7eabae4)
![y](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/872af6ac-2c88-4260-ac12-410b309b7569)

### Lab steps to analyze timing with real clocks using openSTA
To perform timing analysis, instead of invoking separate openSTA tool we will go inside openroad since STA is integrated inside openroad.The benefit of doing this is we are actually inside of openlane and we can use environmental variables. 
![z](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/3cfd804e-1829-4e63-b208-2b3da969b685)
In openroad, timing analysis is performed by first creating db file which is created using lef and def(post CTS def).
![a](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/2c5760cb-cad5-4e67-8437-d48ef5cafe73)Setup slack :
Create db file
![b](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/b9a3055d-e2df-450d-9204-b1412688dff0)
![b](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/b9a3055d-e2df-450d-9204-b1412688dff0)
![d](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/533230db-a898-4bdf-b9ef-1fa83cbef38e)
Setup slack
![e](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/b519dddf-926c-4ec7-994d-7ad4e696e56f)
Hold slack
![f](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/4921b414-6a0b-4cf1-ba68-b0119eec43ca)
Now we have to check whether this analysis is correct or not?
since we have built CTS for typical corner and we have given max and min library during timing analysis in openroad i.e analyzing for slow and fast corner.so this analysis is incorrect.so we will provide typical library in openroad to perform typical corner analysis.
![g](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/28b679b9-b093-4232-86b2-7a32db416bbf)

Setup slack :
![h](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/a203e79f-9d96-4e8c-91db-76d56ec84616)
Hold slack:
![i](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/b2abd71a-8113-44f7-a79d-8e6e71823be0)
So from above results of min_max corner and typical corner analysis we can observe CTS will not have setup and hold violation for typical corner.

Now we will replace synthesis netlist(post cts) with a new for that we will modify buffer list means will remove clk_buf1 from the list and again run CTS and check whether it meets skew value or not.
![j](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/da4a27ac-dd9f-4fff-a170-0bef9127da29)
![k](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/55f20424-55c1-4f1e-bca0-ed341ec757d8)
![l](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/bc72397e-241d-49a9-9890-70eb4e97a1c2)
Since we have use post CTS def file.this is the reason that we have got error.so we need to set current placement def as shown below. 
![m](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/82d06c89-0e02-4f63-b330-ee156f453e4d)
![n](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/cf3541ed-e087-49a0-9cca-6c7425d654b5)
Now again we have to create db
![o](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/d84fdbca-38e7-4148-bc84-96111423e56a)
![p](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/ea455660-3ac7-4d56-8f74-b25c5375cc18)
Setup slack :
![q](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/e46551b3-fdda-477f-9165-0504f4c7356a)
Hold slack :
![r](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/f9ddeb9f-8826-4766-af01-d3316fcba0d1)
So from above results we can observe that setup slack get improved but area increased when we use clkbuf_2 instead of clkbuf_1 and can also see the clkbuf_2 in timing report as shown below
![s](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/99941d47-752f-47fc-ae03-fd6ce32f1118)
Clock skew : It is the time difference between arrival time of clock at two different flop. 
It should be maximum 10% of clock period(12ns).
![t](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/c1cf1cac-1b51-4283-b089-17172799a695)
Inserting clkbuf_1 inside buffer list
![u](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/158bf614-18e4-4207-acb9-e7685b7fa14f)


# Day 5 : Final steps for RTL2GDS using tritonRoute and openSTA
### Lab steps to build power distribution network(PDN)
In openlane PDN is built after CTS stage. gen_pdn is the proc that is used to run PDN.
Issues that I faced while running PDN are:
There are some variables that were not defined in config.tcl such as LIB_SYNTH_COMPLETE Since this variable is called by the proc gen_pdn which is defined in or_pdn.tcl file
And also LEF_MERGED_UNPADDED variable was not set in config.tcl
![v](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/75ef331e-d36c-43ec-9b4e-56b72f3e3746)
Power Planning :
![w](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/17336522-2efe-4560-9d91-305883745891)
Standard cell are in metal1,straps are in metal4 and metal5.
After PDN, current def file i.e picorv32a.cts.def is now changed to pdn.def which has the information about CTS def and PDN.
![x](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/3bda6f8e-6e9d-4157-a2f1-f3bfab5ad5de)

Routing :
Default switches set for routing are :
![y](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/6d169e03-4e4a-448d-af23-673c6459bc0d)
Routing strategy : There are 5 routing strategy
Strategy -- 0,1,2,3,14
Routing strategy 0 means routing will not be converged to zero DRC,but have less runtime and memory requirement.Routing strategy 14 required more runtime and memory requirement.In this design we are using routing strategy 0.
![z](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/8b954ac9-c14d-410c-941d-4771d2b3d0b6)
Entire Routing process is divided into two types :
- Global Route or Fast Route
In global route routing is divided into rectangular grid cells which can be represented as 3D routing graph and it is used durring global route.fast route is basically a engine which performs global route. global route first creates a routing guide i.e boxes(pins of cell) as shown below.so global route output is set of routing guide for each of the net.
Detail Route
Detail route is performed by engine tritonRoute.In detail route we use output from global route i.e routing guide and follow some algorithm to find the best possible connectivity among all this points.
![a](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/23b6d8b9-1cba-4edc-8528-50cae6177147)
![b](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/089d1ac3-76ce-441b-8d56-943e21cd7f28)
In routing alteranate orientation of metal layer is preferred because,If metal1 has non preferred routing direction,it will be parallel to metal2 which can create parallel capacitance so it can degrade the signal. Hence alternate routing direction is preferred.
Two routing guides are connected if:
- They are on the same metal alyer with touching edges.
- They are on neighboring metal layers with a nonzero vertically overlapped area.
![c](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/1b611571-9162-4af8-9041-adac482784b4)
Detail Routes Inputs and outputs :
- Input : LEF,DEF,preprocessed guides
- Outputs:detailed routing soultion wth optimized wire-length via count.
- Constraints : Route guide honoring,connectivity constrains and design rules.
Run_routing
![d](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/3a1000b6-57d6-48f7-a634-29062dd2e506)
![e](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/78e85ec5-4b26-409e-9828-2b62345f26f2)
Routing guides : It is the output of fast route. Detail routing ensures that routing happen within this routing guides.
![f](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/4fd11322-bb67-4684-a627-8694249b01a1)
Can see that for each net there can be many routing guides.
![g](https://github.com/PoojaPatil281/NASSCOM-VSD-SOC-DESIGN-AND-PLANNING/assets/149876515/8d96565d-cccd-468d-8d70-936f1bbc6c09)





