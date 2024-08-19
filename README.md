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







