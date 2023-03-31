# OpenROAD-7nm-Design-Contest
OpenROAD Flow is a full RTL-to-GDS flow built entirely on open-source tools. The tools used in ORFS are yosys,OpenROAD,OpenSTA and KLayout.These tools ensure the design has to meet all the requirements of manufacturing process.

The main aim of the contest was to improve the Power,Performance and Area of the selected Design. The ORFS Flow consist of the following steps:

## 1) Setup-
This stage setup variables to point to other location for the following sub directory. Setup Stage also contains the design and Platform configuration of all design which are defined in OpenROAD FLow Scripts.


## 2) Synthesis-
Synthesis is a process of converting a high-level description of the design into a Technology mapped gate Level Netlist. The main steps of synthesis are Translation,Optimization and Technology Mapping. ORFS performs the Synthesis using the Yosys.


## 3) Floorplan-
The first step of the floorplan is to estimate Die and Core area of the design along with its utilization ratio. After the estimation of aspect ratio and Utilization ratio the tracks are created for the placement of ports,IO pads sites are created for placement of IO pad placement. In floorplan stage the standard cell rows are created for Standard Cell placement and at last the physical cells are added before placement Stage.


## 4) Placement-
