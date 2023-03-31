# OpenROAD-7nm-Design-Contest
OpenROAD Flow is a full RTL-to-GDS flow built entirely on open-source tools. The tools used in ORFS are yosys,OpenROAD,OpenSTA and KLayout.These tools ensure the design has to meet all the requirements of manufacturing process.

The main aim of the contest was to improve the Power,Performance and Area of the selected Design. The ORFS Flow consist of the following steps:

## 1) Setup:
This stage setup variables to point to other location for the following sub directory. Setup Stage also contains the design and Platform configuration of all design which are defined in OpenROAD FLow Scripts.


## 2) Synthesis:
Synthesis is a process of converting a high-level description of the design into a Technology mapped gate Level Netlist. The main steps of synthesis are Translation,Optimization and Technology Mapping. ORFS performs the Synthesis using the Yosys.


## 3) Floorplan:
The first step of the floorplan is to estimate Die and Core area of the design along with its utilization ratio. After the estimation of aspect ratio and Utilization ratio the tracks are created for the placement of ports,IO pads sites are created for placement of IO pad placement. In floorplan stage the standard cell rows are created for Standard Cell placement and at last the physical cells are added before placement Stage.This stage also connects power to the chip by considering issues like EM and IR Drop.

![gui_floorplan ](https://user-images.githubusercontent.com/129440945/229111824-9bbd5778-6cac-445e-9c6e-5ac5064cfcc4.png)



## 4) Placement:
In Placement the standard cells are placed in the rows, usually there are three main stages at placement stages  a) Global Placement b) Legalization c) Timing Optimization. In global placement the standard cells are placed based on the netlist connectivity and the area available. During Legalization, the tool moves the cells to legal locations on the placement grid and eliminate any overlap between the cells.After legalization timing optimizations are done to reduce WNS and TNS.


![gui_place](https://user-images.githubusercontent.com/129440945/229113440-d996891c-1b23-439a-9262-31fa76f70d11.png)



In placement stage the tool tries to do congestion analysis at placement stage, the tool analyses congestion based on the Grid Cells and horizontal and veritical overflow numbers.This overflow mainly occurs due to less no of available tracks as compared to required tracks.



![congestion map ](https://user-images.githubusercontent.com/129440945/229121350-e9f1df51-1fcb-4685-9134-ccfce6644fc7.png)




## 5) CTS:
The main Aim of CTS is to propagate clock to each and every flop in a design with mininmum skew and Latency. While building clock tree the specification files are needed which contains all the information (like list of buffers/Inverters, NDR Rules) that the tools must know to build the Clock tree.


![gui_cts ](https://user-images.githubusercontent.com/129440945/229121445-38fe348e-b1b5-45f1-8506-a815c9eff968.png)


## 6) Routing:
During Routing the actual connects to the standard cells are acheived, these are mainly done in two stages i.e global Routing and detailed Routing. During Global routing the tool defines the shortest routing paths which is not DRC aware, while doing Global Routing the tool tries to assign layers to the nets.In detailed Routing the track assignment is done in which tool assigns each nets to specific metal tracks and in Detailed routing the tools tries to fix all the DRC Violations after track assignment using small Bboxes.

![gui_route ](https://user-images.githubusercontent.com/129440945/229121811-3c67b426-3a99-4310-81fe-fa428ef854d8.png)

## 7) RC Extraction:
In RC Extraction the tool tries to extract the actual net delays which are neccesary for Static Timing Analysis to meet the Setup,Hold Violations and DRV Violations during SignOff.

![gui_final ](https://user-images.githubusercontent.com/129440945/229122401-ac327463-a84b-4341-b8cf-af9c51944083.png)


# Problem Statement:
Comming to the problem Statement the design selected was "ibex" using asap7 PDK, the main agenda of which I worked on was to meet the timing of the design and tried to Optimize the WNS and TNS.

Before reaching to the final result multiple iteration were to optmize the timing using the following commands:

repair_design -max_wire_length max_length
repair_design -slew_margin slew_margin

repair_timing -setup
repair_timing  -hold
repair_timing -repair_tns tns_end_percent

Using the following commands in detail_place.tcl and detail_route.tcl significantly increase the run time of ORFS without optimizing the WNS.

So to Optimize both TNS and WNS the drive Strength of CLK BUFFERS was increased from 4 to 24 and CTS_BUFF_DISTANCE was changed from 60 to 35.

The Changes made in the CONFIG File is shown below using "diff" command:

![difference config](https://user-images.githubusercontent.com/129440945/229107866-7efa0eed-3251-408b-a1fe-439495bc25af.png)

The main reason for upsizing the Clock Buffers was to reduce the cell delay and latency in clock propagation using which reduces skew and inturn reduces the uncertainity leading to better Setup and Hold Optimization.

CTS_BUFF_DISTANCE was reduced because adding buffers at regular interval reduces the risk of minimum pulse width violation and Optimizes the transition violations in the design.

![slack value ](https://user-images.githubusercontent.com/129440945/229111615-385ec8dd-fdc4-4d5f-b2a6-482d3048180c.png)

However due to Upsizing there will be trade off between Power and Timing of the Design. Due to upsizing from "4" to "24" there will be significant increase in Dynamic Power Dissipation. 









