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









