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
