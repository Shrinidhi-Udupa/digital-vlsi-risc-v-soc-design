## digital-vlsi-risc-v-soc-design
# DAY 1 Inception of open-source EDA, OpenLANE and Sky130 PDK
## How to talk to computers

<img width="1512" alt="354795802-a6dcf662-8617-4f0f-a06d-1b0cd34e217e" src="https://github.com/user-attachments/assets/f500dc08-55f8-4636-bd50-ce87b3527303">

<img width="1512" alt="354796072-37b28893-d818-4d90-bee7-387ad797ed4d" src="https://github.com/user-attachments/assets/6f02e251-ecda-40ad-a7ea-9ffc0a6a6c18">

The diagram illustrates a system centered around a Processor/SoC (System on Chip).** This core component is connected to various peripherals and memory modules. It communicates with external devices via direct interfaces like I2C, QSPI, and GPIOs. For memory, it utilizes SDRAM chips, likely for high-speed data access. Additionally, the system includes slower memory options like EEPROM and potentially Flash memory (not explicitly shown). The processor also interacts with debugging and programming interfaces like JTAG and UART. Overall, the diagram provides a high-level overview of the system's architecture, emphasizing the processor's role as the central processing unit.

<img width="1226" alt="354796245-d87efd4b-842c-43d6-81cb-72e7a679c83c" src="https://github.com/user-attachments/assets/c094454a-3f33-4f69-a997-7e9f919b9c61">
The image depicts a top-down view of a QFN-48 package.This type of package is a square, flat package with no leads, commonly used for integrated circuits. The package measures 7mm by 7mm and houses the chip at its center. The chip itself is not visible in this image but is connected to the package's external pins, or pads, through microscopic wire bonds. These pins provide the interface for electrical connections to the chip, enabling communication and power supply. The package also includes markings for orientation and pin identification.

<img width="1214" alt="354796399-9b7c5cc2-1d2a-4418-8f9c-c4ab731357f8" src="https://github.com/user-attachments/assets/2ae55c8c-88a9-4e3c-ae01-1d3175b9a032">
<img width="1221" alt="354796413-e6b41649-06ac-4cdb-a44a-2f106a02345b" src="https://github.com/user-attachments/assets/4a150182-1da8-4dcc-b694-657663408e43">

Chip Layout

The image illustrates a top-down view of a chip's architecture.

Core: At the center lies the RISC-V SoC (System on Chip), the chip's core processing unit.

Peripherals: Surrounding the core are various functional blocks, including a GPIO bank for general input/output, SRAM for fast data storage, and an unspecified block labeled "comp_inn."

Pads: The chip's outer perimeter is lined with pads, the physical connection points for power supply (VDD), ground (VSS), clock signals (CLK), and data transfer (e.g., flash_io, ser_tx, ser_rx).

Foundry IP's and Macros: While not visually distinct in this image, the chip likely incorporates pre-designed building blocks from the foundry and custom-designed macros to enhance its functionality.

# Introduction to RISC V

<img width="1459" alt="354796556-ed8c3d00-53db-4062-9b08-e20bef811971" src="https://github.com/user-attachments/assets/d074b903-9d1c-4fc4-927f-0ebe241df8db">

The image provides a snapshot of the RISC-V development process. On the left, a code editor displays C code implementing a "swap" function, which will be compiled into machine code. The middle section shows the assembly code generated for the "swap" function, revealing the RISC-V instructions used. On the right, a block diagram outlines the architecture of a potential RISC-V implementation, the "picorv32" core, detailing its components and control logic. The image underscores the relationship between high-level code, assembly language, and the underlying hardware architecture in the context of RISC-V.

<img width="1458" alt="354797154-3d986af3-f230-4935-b941-1e3a9d6d2dfd" src="https://github.com/user-attachments/assets/a3f2c8c6-e078-46d8-a59a-a96a24cc46b1">

The image illustrates the design flow from high-level software instructions to physical hardware implementation in a RISC-V processor. Starting with assembly code representing an "add" instruction, the assembler converts it into machine code. This machine code, representing the Instruction Set Architecture (ISA), serves as an abstract interface to the hardware. The RTL (Register Transfer Level) code, written in a hardware description language, defines the logic for processing these instructions. This RTL is then synthesized into a netlist, a detailed description of the circuit's components and connections. Finally, the physical design implementation translates the netlist into a layout of transistors and wires on a silicon chip, creating the actual hardware capable of executing the original "add" instruction. 

# SoC design and OpenLANE

Introduction to all components of open-source digital asic design

<img width="1411" alt="354802750-aca4a2b1-0974-4a30-b7ff-d4018d504f54" src="https://github.com/user-attachments/assets/7c75462a-13c3-4eb7-a81b-677640c73e5a">


1. EDA Tools:

qflow: This is the overall flow manager orchestrating the entire design process. It handles task scheduling, resource allocation, and data management. OpenROAD: A comprehensive tool suite covering various design stages, including synthesis, placement, and routing. It optimizes the chip layout for performance and power efficiency. OpenLANE: A complete flow for digital ASIC implementation, encompassing tasks like synthesis, physical design, and sign-off. It provides a streamlined approach to the design process.

2. RTL Designs:

These are the initial designs written in hardware description languages like Verilog or VHDL. They capture the chip's functionality at a high level. librecores.org, opencores.org, and github.com: These platforms offer a rich repository of open-source RTL designs for various components, accelerating the design process.

3. PDK Data:

Process Design Kit (PDK): This essential data package provides detailed information about the manufacturing process, including transistor models, design rules, and library cells. Google Skywater PDK: A prominent open-source PDK for a 130nm process, enabling the fabrication of chips through Skywater Technology Foundry.

# Simplified RTL2GDS flow

<img width="1407" alt="354802844-ef8f56a6-e030-4ddf-aaa0-ba7a9aa9dd3b" src="https://github.com/user-attachments/assets/dd2832e8-5eca-4359-8353-e64631188ca0">


1. RTL (Register Transfer Level):

This is the starting point, where the design is captured in a hardware description language like Verilog or VHDL. It represents the high-level behavior of the circuit, defining how data is transferred between registers.

2. PDK (Process Design Kit):

Contains detailed information about the manufacturing process, including transistor models, design rules, and library cells. Essential for ensuring the design is compatible with the chosen fabrication technology.

3. GDSII:

The final output, a file format containing the geometric data used to manufacture the integrated circuit (IC). Flow Stages:

Synthesis:

Translates the RTL design into a gate-level netlist, representing the circuit using logic gates. Optimization tools are used to minimize area, power consumption, and delay. Floorplanning (FP) and Power Planning (PP):

Determines the overall chip layout, including the placement of major functional blocks and power distribution networks. Ensures efficient power delivery and ground connections. Placement:

Assigns physical locations to individual logic gates and standard cells within the chip area. Optimization algorithms aim to minimize wire length and delay. Clock Tree Synthesis (CTS):

Designs the clock distribution network, ensuring that all clock signals arrive at flip-flops with minimal skew and jitter. Critical for timing closure and circuit performance. Routing:

Connects the logic gates and other components using metal wires within the chip layers. Routing algorithms optimize wire length, congestion, and signal integrity. Sign-Off:

Verifies that the final design meets all design constraints and requirements. Includes static timing analysis (STA), power analysis, and layout verification.

# Introduction to OpenLANE and Strive chipsets

<img width="1406" alt="354803057-17a8ae36-b90f-4740-b6fb-96afcf0cf1ac" src="https://github.com/user-attachments/assets/80defcde-05a5-4cf3-add1-f5105989aecf">

Main Goal

The primary objective of the OpenLANE flow is to automate the entire ASIC design process from RTL to GDSII without requiring human intervention. This is a significant step towards achieving a fully autonomous design flow.

Definition of a "Clean" GDSII

A "clean" GDSII, as defined in the image, adheres to the following criteria:

No LVS Violations: Logical and physical representations of the design must match perfectly. No DRC Violations: The design must comply with all design rules specified by the fabrication process. Timing Violations: Currently under development (WIP). Achieving timing closure without manual intervention is a challenging but crucial goal. Significance of OpenLANE

By striving for a completely automated flow with a clean GDSII output, OpenLANE aims to streamline the ASIC design process, reduce time-to-market, and minimize design errors. This aligns with the broader industry trend towards increased design automation and reduced reliance on human expertise.

In essence, the image highlights OpenLANE's ambition to become a fully autonomous ASIC design platform capable of producing high-quality, manufacturable designs without human intervention.

# Introduction to OpenLANE ASIC flow

<img width="1405" alt="354803182-8b705ab2-4c9f-45a1-bf3e-670306a94d4c" src="https://github.com/user-attachments/assets/6b60c620-fdd2-4487-b559-1b633d238481">

OpenLANE ASIC flow is a comprehensive, open-source framework designed to automate the entire process of creating an integrated circuit (IC) from Register Transfer Level (RTL) code to a manufacturable GDSII file. It encompasses a wide range of design stages, from synthesis and floorplanning to physical verification.

Key Components and Stages

1. Design Input:

RTL: The initial design is captured in RTL code, typically using Verilog or VHDL. This code describes the circuit's functionality at a high level. PDK (Process Design Kit): Provides detailed information about the manufacturing process, including transistor models, design rules, and standard cell libraries. It ensures compatibility between the design and the fabrication technology.

2. Synthesis:

RTL Synthesis: The RTL code is translated into a gate-level netlist using tools like Yosys and ABC. This netlist represents the circuit using logic gates. Synthesis Exploration: Multiple synthesis options are explored to find the best trade-offs between area, power, and performance.

3. Floorplanning:

OpenROAD App: This tool is used for initial chip layout planning. It determines the placement of major functional blocks and power distribution networks. Placement:

The logic gates and standard cells are assigned specific physical locations within the chip area. Optimization algorithms are employed to minimize wire length and delay.

4. Power Planning:

The power distribution network is designed to ensure efficient power delivery and ground connections throughout the chip.

5. Clock Tree Synthesis (CTS):

The clock distribution network is generated to deliver clock signals to all flip-flops with minimal skew and jitter. This is crucial for timing closure.

6. Optimization:

Various optimization techniques are applied to improve design characteristics such as area, power, and performance.

7. Detailed Routing:

The physical connections between logic gates and other components are established using metal wires within the chip layers. Routing algorithms aim to minimize wire length, congestion, and signal integrity.

8. Static Timing Analysis (STA):

The timing performance of the design is analyzed to ensure it meets the specified timing constraints. OpenSTA is used for this purpose.

9. Physical Verification:

The design is checked for errors such as layout versus schematic (LVS) mismatches and design rule checks (DRC) violations. Tools like Magic and Netgen are employed.

10. Design for Testability (DFT):

Structures are added to the design to enable testing and fault diagnosis.

11. GDSII Output:

The final design is converted into a GDSII file, which is the standard format for manufacturing data

## Get familiar to open-source EDA tools
# OpenLANE Directory structure in detail

OpenLANE: Streamlining Your Design Journey

OpenLANE leverages a collection of open-source Electronic Design Automation (EDA) tools. Its primary purpose is to automate the entire process of transforming your Register Transfer Level (RTL) code into a GDSII file, ready for chip manufacturing.

Navigating Your Design Workflow:

![354837891-8ccf7f40-3214-404f-8576-3e988fd7b24b](https://github.com/user-attachments/assets/b1addfd5-efb6-4f07-9b30-3ebf40a4458f)

Here's a step-by-step guide using Linux commands to navigate OpenLANE project:

Locate Your Tools:

1. Begin by opening a terminal and navigate to your tools directory using the command cd Desktop/work/tools. Access Your Working Directory:

2. Next, move to your specific OpenLANE project directory with cd openlane_working_dir. Explore the PDK (Process Design Kit):

3. To delve into the Sky130A process details, enter cd pdks/sky130A/. This directory contains information about the chip fabrication process. View PDK Files:

4. To see a list of files related to Sky130A (ordered by date with the newest at the top), use ls -ltr. Locate Reference Library Files:

5. Access the directory containing reference library files specific to the chosen process with cd libs.ref. Review Reference Library Files:

6. Utilize ls -ltr again to view the files within the libs.ref directory. Explore Tool-Specific Library Files:

7. Navigate back one level using cd .. and then move to the libs.tech directory containing files specific to the OpenLANE tools themselves. Check Tool-Specific Library Files:

8. Finally, use ls -ltr one last time to list the files in the libs.tech directory.

![354838142-f637e0cd-7b58-4d8c-b253-940bb4ba2474](https://github.com/user-attachments/assets/75733a92-ba87-4c3a-820a-56a9d8722553)

Viewing Library Files:

1. Process-Specific Files (libs.ref):
        Use cd libs.ref to access the directory containing reference library files specific to the chosen chip fabrication process.
        Run ls -ltr to list all files within libs.ref, sorted by date with the newest at the top.

2. Tool-Specific Files (libs.tech):
        Navigate back one directory level using cd ...
        Enter cd libs.tech to move to the directory containing files specific to the OpenLANE tools themselves.
        Finally, use ls -ltr again to list all files in libs.tech.

### SK3 - Lecture2
#### Design Preparation Step

To enter into bash while being in the openalne dircetory use the command

*** 
docker
***
Now after this we use the script 'flow.tcl' and alongwith it use '-interactive' for the step by step openlane flow. :
***
./flow.tcl -interactive
***
![Screenshot 2024-07-13 160109](https://github.com/user-attachments/assets/c87a942c-bd0a-447c-9958-0aad7e2cc066)
Openlane Logo can be seen in the terminal which is affirmative , after this enter the following command to install require openlane packages
***
% package require openlane 0.9
***
Now, Ther are various pre-built designs in the 'designs' subdirectory. So, here we are selecting the "picorv32a.v" design on which we will execute the RTL to GDS flow. To carry out the synthesis (the project's initial stage) on this design, we first need to set it up using the command:
***
prep -design picorv32a
run_synthesis
***
![Screenshot 2024-07-13 162118](https://github.com/user-attachments/assets/84b6b5a1-f243-45e4-841f-fe2dea463e17)
After the preparation is complete, we can see a new directory with todays date is created within 'runs' folder in 'picorv32a' folder.

### Key Sections and Variables:
Design Setup:

1. Design
***
set ::env(DESIGN_NAME) "picorv32a"
set ::env(VERILOG_FILES)  "~/designs/picorv32a/src/picorv32a.v" 
set ::env(SDC_FILE) "~/designs/picorv32a/src/picorv32a.sdc"
***
DESIGN_NAME: Sets the design's name to picorv32a.

VERILOG_FILES: Specifies the path to the Verilog file containing the picorv32a design.

SDC_FILE: Indicates the path to the Synopsys Design Constraints (SDC) file, which contains timing constraints for the design.

2. Clock Configuration:
***
 set ::env(CLOCK_PERIOD)  "5.000"
 set ::env(CLOCK_PORT) "clk"
 set ::env(CLOCK_NET)  $::env(CLOCK_PORT)
***
 CLOCK_PERIOD: Defines the desired clock period for the design as 5 nanoseconds.

CLOCK_PORT: Sets the name of the clock input port to clk.

CLOCK_NET: Assigns the clock net to be the same as the clock port.

3. Configuration File Inclusion:
***
 set filename $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/$::env(PDK)/$::env(STD_CELL_LIBRARY)_config.tcl 
   if {[file exists $filename] == 1} {
     source $filename
       }
***
This section constructs a filename based on environment variables to include a technology-specific configuration file.

It sources (includes) this file if it exists, potentially containing PDK-specific settings.
![Screenshot 2024-07-13 160719](https://github.com/user-attachments/assets/b717398c-b384-4883-8263-e439bf6bb233)

4. Standard Cell Library (SCL) Configurations:

SCL Configs
***
set ::env(GLB_RT_ADJUSTMENT) 0.1
set ::env(SYNTH_MAX_FANOUT) 6
set ::env(CLOCK_PERIOD) "24.73"
set ::env(FP_CORE_UTIL) 35
set ::env(PL_TARGET_DENSITY) [ expr ($::env(FP_CORE_UTIL)+5) / 100.0 ]
***
This part defines various configuration parameters for the standard cell library being used:

GLB_RT_ADJUSTMENT: Global routing tree adjustment.

SYNTH_MAX_FANOUT: Maximum fanout allowed during synthesis.

CLOCK_PERIOD: Overwrites the previous clock period setting.

FP_CORE_UTIL: Specifies core utilization for floorplanning.

PL_TARGET_DENSITY: Sets the target density for placement.

![Screenshot 2024-07-13 161133](https://github.com/user-attachments/assets/8f280309-dcfd-4d43-9a9b-787db2f8459f)

## SK3 - Lecture3
### Inside an OpenLANE Design: Directory Structure and PDK Integration:

Screenshot 1 (Directory Structure):

The user navigates to a specific design directory within an OpenLANE project: .../openlane/designs/picorv32a/runs/13-07_10-49

Key Subdirectories:

PDK_SOURCES: Contains links or copies of files directly from the Skywater PDK.

results: Stores the output files generated during various stages of the OpenLANE flow. Further subdirectories like synthesis, placement, routing, lvs indicate where results for each stage are stored.

logs: Contains log files capturing the execution details of each step.

config.tcl: This crucial file likely holds design-specific configurations and settings for OpenLANE tools.


Screenshot 2 (PDK License):

Shows the contents of the merged.lef file within the PDK_SOURCES directory.The header clearly states that it's part of the Skywater PDK and released under the Apache License 2.0.This file likely contains Library Exchange Format (LEF) data, providing physical layout information about the standard cells within the PDK.

Screenshot 3 (Design Configuration):

Displays a snippet of the run.cfg file, a primary configuration file for OpenLANE.

PDK Integration: set ::env(PDK_ROOT) ...: Sets the root directory of the Skywater PDK, allowing OpenLANE tools to access its contents.

Design-Specific Settings:

Specifies various paths to design files (SDC, LEF), clock parameters, cell padding/exclusion rules, and more. It demonstrates how OpenLANE allows for fine-grained control over the ASIC design flow through Tcl configuration.

## SK3 - Lecture4
### OpenLANE Git: Your Gateway to Open-Source ASIC Design

Key Repositories:

    Main OpenLANE Repository:

     URL: https://github.com/The-OpenROAD-Project/OpenLANE

This is the central hub for OpenLANE, containing the core infrastructure, scripts, flow configurations, and documentation.

    Skywater PDK (Sky130):

     URL: https://github.com/google/skywater-pdk

This repository hosts the Google-sponsored Skywater 130nm Process Design Kit (PDK), often used with OpenLANE.

Other PDK Repositories: You can find PDKs from other foundries on GitHub or other platforms.

Common Git Commands for OpenLANE:

git clone: Download a copy of the OpenLANE or PDK repository to your local machine.

git pull: Update your local repository with the latest changes from the remote repository.

git checkout: Switch between different branches or versions of the code.

git diff: View the changes you've made to files.

git add, git commit, git push: Stage, commit, and push your changes to a remote repository (e.g., on GitHub).

## SK3 - Lecture5
### OpenLANE Results Analysis: Cell Counts/Flop calculation and Directory Exploration

Screenshot 1 (Directory Navigation and Files):

Results Directory: The user navigates to the synthesis subdirectory within the OpenLANE run's results folder: .../openlane/designs/picorv32a/runs/13-07_13-33/results/synthesis.

Key Files: merged_unpadded.lef: This Library Exchange Format (LEF) file likely contains the physical layout information for the standard cells used in the design, potentially after merging multiple libraries.

picorv32a.synthesis.v: Represents the synthesized netlist of the picorv32a design in Verilog format. This netlist is the output of the synthesis stage, mapping the original RTL design to the chosen standard cells.

![Screenshot 2024-07-13 191251](https://github.com/user-attachments/assets/7dd9afa1-4a27-4302-8a87-35112e1cc0df)

Screenshot 2 (Design Statistics):

Cell Counts: The output highlights the count of different standard cells used in the design, grouped by cell type (e.g., sky130_fd_sc_hd_a211o_2, sky130_fd_sc_hd_a21bo_2).

Area Estimation: Different cells have varying sizes, so cell counts provide an initial estimate of the design's area.
Performance Analysis: Cell complexity influences timing characteristics; analyzing cell types helps understand potential performance bottlenecks.

Now, coming back to the step where design preperation was completed successfully. Now, To perform synthesis on the design use the following command :

  % run_synthesis

Now, First objective after the synthesis is completed is to calculate the Flip Flop Ratio.

Now, if we see the synthesized results we find:

Number of D Flipflops : 1613
Total number of Cells : 14876
![Screenshot 2024-07-13 191025](https://github.com/user-attachments/assets/4f78a401-8033-43fa-8b90-3de7b3d0482d)

FF Ratio : 0.1084
FF Percentage : 10.84 %

Hence, flip flop ratio = (Number of D Flipflops)/(Total number of Cells) Flipflop percentage = FF ratio * 100

## DAY-2

### SK1- Lecture1
Understanding Chip Area, Core, Die, and Utilization Factor

This series of diagrams provides a visual explanation of key concepts related to chip design, focusing on the core, die, utilization factor, and aspect ratio.
Slide 1: Determining Core Dimensions and Utilization

1. Explains that the core's dimensions are determined by the placement of all logic cells within it.

2. 100% utilization occurs when all logic cells completely fill the core area.

3. The utilization factor is calculated by comparing the area occupied by cells to the total core area.

![Screenshot 2024-07-14 185039](https://github.com/user-attachments/assets/6f681647-218a-4419-979f-5ad44e8a5168)

OpenLANE Configuration and Execution: Defining Variables and Observing the Flow

Screenshot 1 (Configuration Variables):

Configuration File (config.tcl): This snippet showcases a portion of OpenLANE's configuration file where essential design parameters are defined.

Required Variables: It highlights "required variables" crucial for a successful run.

    DESIGN_NAME: Specifies the top-level module name of your design.

    VERILOG_FILES: Provides the path(s) to your Verilog design files.

    CLOCK_PERIOD: Defines the clock period in nanoseconds.

    CLOCK_NET and CLOCK_PORT: Specify clock-related information used in different stages (CTS, STA).

![Screenshot 2024-07-15 161206](https://github.com/user-attachments/assets/567c9ecf-c182-4325-b524-3974a816255b)

Screenshot 2 (Configuration Directory):

OpenLANE Configuration Directory: Shows the contents of OpenLANE's configuration directory.

Tcl Scripts for Different Stages: The directory contains individual Tcl scripts (synthesis.tcl, placement.tcl, routing.tcl, etc.) that define the flow for each design stage.

![Screenshot 2024-07-15 161414](https://github.com/user-attachments/assets/5e57b86f-51e0-4ced-9728-804e7257021e)

OpenLANE Design Flow: Navigating Directories, Examining Floorplan Data, and Visualizing Layout

Screenshot 1-2 (Project Directory Exploration):

The user navigates through various directories within an OpenLANE project, ultimately reaching:

A specific run directory:

          .../openlane/designs/picorv32a/runs/15-07_10-57

The results/floorplan subdirectory containing output files from the floorplanning stage.

Key Subdirectories:

1. PDK_SOURCES: Holds links to the Skywater PDK files used in the design.
2. results: Stores outputs from different stages (e.g., synthesis, floorplan, routing).
3. logs: Contains log files for each stage's execution.

![Screenshot 2024-07-15 163108](https://github.com/user-attachments/assets/43dae03c-a73c-4e53-b6fc-128ecabf1021)

Key Information:

VERSION: DEF file version.
DESIGN: The name of the design (picorv32a).
DIEAREA: Specifies the dimensions of the chip's die area.
ROW: Defines the rows available for placing standard cells, with their coordinates, orientation, and spacing.

![Screenshot 2024-07-15 163748](https://github.com/user-attachments/assets/13d06a8b-cfc1-4fb9-81ff-8990224ca7b2)

Calculator to convert the die area dimensions from the DEF file (6606685 x 671405) into units representing microns.

![Screenshot 2024-07-15 163857](https://github.com/user-attachments/assets/7ad50da1-e380-4fdd-9af3-e6c08107b048)

The floorplan is visualized using a layout viewer tool (possibly klayout).

Key Observations:

1. Die Area: The overall rectangular area represents the chip die.
2. Rows: The repeating vertical lines likely represent the rows defined in the DEF file for cell placement.
3. Pre-Placed Blocks: There might be (though not clearly visible in this screenshot) rectangular areas representing pre-placed blocks like memories or macro cells.

![Screenshot 2024-07-15 164728](https://github.com/user-attachments/assets/80a9dab6-f50e-4330-ad3c-5ebb921002b3)

Exploring Standard Cell Details in a Layout Viewer

Screenshot 1 (Standard Cell Properties):

1. Layout Viewer: The main window displays a section of the ASIC layout.
2. Tcl Console: The console provides a command-line interface for interacting with the layout data.
3. Cell Details: The user has likely selected a standard cell, triggering the display of its properties:
4. Name: The cell is identified as pcpi.
5. Size: It occupies an area of 8.018 microns x 8.018 microns.
6. Layers: Information about metal layers (Metal1, Metal2) and their connections to the pcpi cell's pins.
7. Label Attachment: It shows specific labels ("pcpi_rd/I1") are associated with metal connections to this cell instance.

![Screenshot 2024-07-15 165243](https://github.com/user-attachments/assets/e041901d-f2ed-4c95-aa75-b21b041eafad)

Purpose:

Standard Cell Structure: Examining the pcpi cell's physical layout, including its size and connections to different metal layers.

Label Verification: Confirming the correct association of labels (e.g., "pcpi_rd/I1") with specific metal traces connected to the pcpi cell.

Connectivity Analysis: Understanding how this cell is connected to the surrounding circuitry through the labeled metal traces.

### OpenLANE Design Flow: Placement Statistics, Directory Organization, and Visualization

Screenshot 1 (Placement Statistics):

    Log Messages: The terminal window displays log messages from the OpenLANE run, providing statistics about the placement process:
    Design Area: Total area, utilized area, and utilization percentage.
    Cell Counts: Numbers of different cell instances and total instances.
    Placement Metrics: Data related to cell displacement, wirelength, and HPWL (Half-Perimeter Wirelength), which are indicators of placement quality.

run_placement

![Screenshot 2024-07-15 175722](https://github.com/user-attachments/assets/7a7b96ec-78fb-44dc-a7e2-e657d91995d6)

 The user navigates through the OpenLANE project directory, highlighting the placement subdirectory within a specific run's results folder (.../openlane/designs/picorv32a/runs/15-07_12-25/results/placement). Purpose: This navigation indicates that the placement results, including placement data and log files, are organized by design and run within the results directory.

 picorv32a.placement.def

the above file contains the info about placement.

Placement Display: A layout viewer (tkcon) visualizes the placement of standard cells within the picorv32a design. Cell Instances: Individual standard cells are likely represented by rectangles or other shapes, but their specific details are not clearly visible in this screenshot. Console Output: The console window suggests that the viewer is loading the design's netlist and technology information for accurate visualization.

navigate to tool by the following command:

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

![Screenshot 2024-07-15 181533](https://github.com/user-attachments/assets/012f3209-3068-4991-8f87-73fa01abf715)

A zoomed-in view of the layout after placement is presented, showing: Standard Cells: The rectangles likely represent individual standard cell instances placed on the layout. Labels: Some cells have labels indicating their types or functions (e.g., _19458, _19321). Routing Tracks: Faint lines in the background might represent the available routing tracks for interconnecting the cells.

![Screenshot 2024-07-15 182128](https://github.com/user-attachments/assets/873dbfe4-33ba-4b00-99a8-cc7aecaf0ce4)

for more controls use these commands:

# Design Alignment Instructions

## Centering the Design

1. Press `S` to select the entire design.
2. Press `V` to vertically align it to the middle of the screen.

## Zooming In on a Specific Area

1. Left-click and drag to select the desired region.
2. Right-click to bring up the context menu.
3. Press `Z` to zoom in on the selected area.

## Getting Details of a Cell

1. Move your cursor to the cell of interest.
2. Press `S` to select the cell.
3. In the `tkcon` window, enter the command `what` to display cell details.

# Day 3

Configuring Parameters and Visualizing Results

This set of screenshots demonstrates how floorplanning parameters can be customized in OpenLANE using Tcl variables and how the resulting floorplan is visualized for a picorv32a design.

Screenshot 1 (Floorplan Configuration):

Tcl Variables: Shows a section of a Tcl configuration file (config.tcl or similar) dedicated to floorplanning settings.

Key Parameters:

    FP_IO_VMETAL, FP_IO_HMETAL: Specify metal layers for vertical and horizontal IO connections.
    FP_SIZING, FP_CORE_UTIL, FP_ASPECT_RATIO: Control overall floorplan sizing, core utilization, and aspect ratio.
    FP_PDN_* variables: Define parameters related to the power distribution network (PDN) like offsets, pitches, and adjustments.
    FP_IO_MODE, FP_IO_HLENGTH, etc.: Configure input/output (IO) placement parameters.

![Screenshot 2024-07-15 192134](https://github.com/user-attachments/assets/36d67eb3-daa9-4118-935a-633bd47f97e2)

OpenLANE Log: The terminal displays log messages from an OpenLANE run.

Floorplan Execution: Highlights the execution of therun_floorplan, indicating the start of the floorplanning stage.

Layout Visualization: Shows OpenLANE invoking a layout viewer (klayout in this case) to display the generated floorplan.

set  ::env(FP_IO_MODE) 2
run_floorplan

![Screenshot 2024-07-15 192348](https://github.com/user-attachments/assets/5023d463-f388-4720-af16-83ce6e1584ee)

Floorplan Visualization:

1. Layout Viewer Display: Presents the visualized floorplan within the layout viewer.
2. Core Area: A central rectangular area represents the core of the design where standard cells are placed.
3. IO Pads: There might be regions around the core dedicated to IO pads for external connections.
4. Power Grid: A grid-like structure might be visible, indicating the power distribution network.

Here the IO Pin arrangement is changed now to 2 previouly it was set to 1 as default and was divided in equal manner

![Screenshot 2024-07-16 001813](https://github.com/user-attachments/assets/db653f77-5c9b-408b-9783-0e9b2a13f83d)

![Screenshot 2024-07-15 192134](https://github.com/user-attachments/assets/6947c708-f723-4d5e-ab55-7890d4c5875c)

![Screenshot 2024-07-15 192348](https://github.com/user-attachments/assets/f2ea4f4c-e2a0-48a3-8107-8fa933ed9a39)

![Screenshot 2024-07-16 181716](https://github.com/user-attachments/assets/31b8b8f1-f309-41d3-9fa6-08ecf9bf5ea9)

![Screenshot 2024-07-16 194152](https://github.com/user-attachments/assets/5054d543-7003-4ea3-8e02-e9cce96dd3d6)

![Screenshot 2024-07-16 194927](https://github.com/user-attachments/assets/9329b913-6b45-4123-b364-7ce3b40e8f20)

![Screenshot 2024-07-16 195418](https://github.com/user-attachments/assets/59d31ebc-bd89-4013-8269-e0eb09c6dd3b)

![Screenshot 2024-07-16 195615](https://github.com/user-attachments/assets/adda1ed9-6da9-4cd8-9b69-c4432344b85d)

![Screenshot 2024-07-16 225203](https://github.com/user-attachments/assets/1de2b6a2-f0a7-4b6a-bc89-5aea9e301b9f)

![Screenshot 2024-07-16 231009](https://github.com/user-attachments/assets/033b68a9-4cf5-4cae-8ff7-439983b93ee6)

![Screenshot 2024-07-16 231111](https://github.com/user-attachments/assets/306c388c-519a-4fdf-8eac-3883f8070b0d)

![Screenshot 2024-07-16 233138](https://github.com/user-attachments/assets/14e96db8-03d6-4ac4-96c7-41273b0d757a)

![Screenshot 2024-07-16 233214](https://github.com/user-attachments/assets/85b3d429-42ea-440e-afbc-df979788ee9e)

![Screenshot 2024-07-16 233227](https://github.com/user-attachments/assets/41650de9-ea1b-4906-8659-43e25c7faf57)

![Screenshot 2024-07-17 091937](https://github.com/user-attachments/assets/182a05f9-6d16-4f25-a028-575eee9333de)

![Screenshot 2024-07-17 095021](https://github.com/user-attachments/assets/9388f158-0e98-41ec-a6bc-ccd10a4c7cea)

![Screenshot 2024-07-17 095150](https://github.com/user-attachments/assets/d090f50b-7ccf-4f23-a5b5-b74b4f2dc6c5)

![Screenshot 2024-07-17 104547](https://github.com/user-attachments/assets/edd49f37-cc30-4596-8ac7-619e06a5745d)

![Screenshot 2024-07-17 105212](https://github.com/user-attachments/assets/21b0f1ae-70a9-4993-bf86-19a1197c186b)

![Screenshot 2024-07-17 105459](https://github.com/user-attachments/assets/331e650a-4f30-4cab-8caf-8d962b496c72)

![Screenshot 2024-07-17 110530](https://github.com/user-attachments/assets/cd729033-2e44-4f10-995c-7a9f6977a1a9)

![Screenshot 2024-07-17 124417](https://github.com/user-attachments/assets/6bf2d0a7-693e-434a-b092-88295ad0f6b3)

![Screenshot 2024-07-17 130236](https://github.com/user-attachments/assets/8e49c45b-d234-4033-ba44-726096e238cd)

![Screenshot 2024-07-17 135153](https://github.com/user-attachments/assets/a0440971-ac1e-4838-908e-8a4390e9f43b)

![Screenshot 2024-07-17 143612](https://github.com/user-attachments/assets/91f23027-1468-4df3-ac2e-b661069529cc)

![Screenshot 2024-07-17 144434](https://github.com/user-attachments/assets/bac4b709-2488-4c92-acb4-5a133f15e817)

![Screenshot 2024-07-17 172332](https://github.com/user-attachments/assets/b6058900-ca1f-4689-8b48-a3709d2a7e95)

![Screenshot 2024-07-17 195920](https://github.com/user-attachments/assets/65183b20-19d5-4d3e-8825-01000945ad1d)

![Screenshot 2024-07-18 113833](https://github.com/user-attachments/assets/f9244632-9f3d-44d9-b2c6-b41d46cbb32d)

![Screenshot 2024-07-18 113847](https://github.com/user-attachments/assets/887ef841-b66a-4638-8d0e-553845357900)

![Screenshot 2024-07-18 114938](https://github.com/user-attachments/assets/634c5b8b-6271-4415-99d1-11528bdd6afd)

![Screenshot 2024-07-18 122737](https://github.com/user-attachments/assets/ce24d0bb-f922-4b79-bb88-828bd41dc038)

![Screenshot 2024-07-18 122755](https://github.com/user-attachments/assets/3a05162b-1fe7-4ca7-883e-720c812e6c1f)

![Screenshot 2024-07-18 124334](https://github.com/user-attachments/assets/44ebf4da-2b0c-4fb4-a9f5-e400577eb6e3)

![352796869-8d6eda4d-5aa6-4d4e-ba5b-742acb3864bf](https://github.com/user-attachments/assets/a51cea16-6f9d-4235-b5fb-2d8b189edd50)

![352796868-a653c05e-5740-4b73-b1b4-454cedaabeaf](https://github.com/user-attachments/assets/2e16c26b-fad9-4a84-b4ec-03841ebaec1c)















