# OpenROAD-7nm-Design-Contest
OpenROAD Flow is a full RTL-to-GDS flow built entirely on open-source tools. The tools used in ORFS are yosys,OpenROAD,OpenSTA and KLayout.These tools ensure the design has to meet all the requirements of manufacturing process.

The main aim of the contest was to improve the Power,Performance and Area of the selected Design. The ORFS Flow consist of the following steps:

## 1) Setup:
This stage setup variables to point to other location for the following sub directory. Setup Stage also contains the design and Platform configuration of all design which are defined in OpenROAD FLow Scripts.


## 2) Synthesis:
Synthesis is a process of converting a high-level description of the design into a Technology mapped gate Level Netlist. The main steps of synthesis are Translation,Optimization and Technology Mapping. ORFS performs the Synthesis using the Yosys.


## 3) Floorplan:
The first step of the floorplan is to estimate Die and Core area of the design along with its utilization ratio. After the estimation of aspect ratio and Utilization ratio the tracks are created for the placement of ports,IO pads sites are created for placement of IO pad placement. In floorplan stage the standard cell rows are created for Standard Cell placement and at last the physical cells are added before placement Stage.This stage also connects power to the chip by considering issues like EM and IR Drop.


## 4) Placement:
In Placement the standard cells are placed in the rows, usually there are three main stages at placement stages  a) Global Placement b) Legalization c) Timing Optimization. In global placement the standard cells are placed based on the netlist connectivity and the area available. During Legalization, the tool moves the cells to legal locations on the placement grid and eliminate any overlap between the cells.After legalization timing optimizations are done to reduce WNS and TNS.


## 5) CTS:
The main Aim of CTS is to propagate clock to each and every flop in a design with mininmum skew and Latency. While building clock tree the specification files are needed which contains all the information (like list of buffers/Inverters, NDR Rules) that the tools must know to build the Clock tree.


## 6) Routing:
During Routing the actual connects to the standard cells are acheived, these are mainly done in two stages i.e global Routing and detailed Routing. During Global routing the tool defines the shortest routing paths which is not DRC aware, while doing Global Routing the tool tries to assign layers to the nets.In detailed Routing the track assignment is done in which tool assigns each nets to specific metal tracks and in Detailed routing the tools tries to fix all the DRC Violations after track assignment using small Bboxes.

## 7) RC Extraction:
In RC Extraction the tool tries to extract the actual net delays which are neccesary for Static Timing Analysis to meet the Setup,Hold Violations and DRV Violations during SignOff.

# Problem Statement:
Comming to the problem Statement the design selected was "ibex" using asap7 PDK, the main agenda of which I worked on was to meet the timing of the design and tried to Optimize the WNS and TNS.

Before reaching to the final result multiple iteration were to optmize the timing using the following commands:
