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
