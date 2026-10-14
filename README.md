# RTL Design and FPGA Implementation of an AXI4-Lite Slave Interface for AMBA-Based SoC Applications

## 1. Project Overview

This project focuses on the RTL design and FPGA implementation of an AXI4-Lite slave interface for AMBA-based System-on-Chip (SoC) applications using Verilog HDL and AMD Vivado.

AXI4-Lite is a lightweight interface protocol designed for simple memory-mapped register transactions. It is commonly used to connect processors and control logic with peripheral registers in SoC architectures.

The project involves developing separate RTL modules for the AXI4-Lite communication channels, simulating their behavior, debugging the design, and preparing it for FPGA implementation.

## 2. Aim

To design and implement an AXI4-Lite slave interface using Verilog HDL and evaluate its operation through RTL simulation and FPGA implementation.

## 3. Objectives

- Study the AMBA AXI4-Lite protocol and its communication mechanism.
- Design modular RTL using Verilog HDL.
- Implement address, data, and response handling for read and write transactions.
- Understand and implement VALID/READY handshaking.
- Develop testbenches for functional simulation.
- Debug the RTL modules using AMD Vivado.
- Integrate the individual modules into a complete slave interface.
- Synthesize and implement the design on the target FPGA board.
- Observe and analyze the hardware output.

## 4. AXI4-Lite Protocol

AXI4-Lite is a simplified, memory-mapped communication protocol derived from the AMBA AXI family. It is suitable for register-based control and status operations.

The protocol uses five independent channels:

| Channel | Purpose |
|---|---|
| Write Address (AW) | Transfers the write address |
| Write Data (W) | Transfers write data and byte strobes |
| Write Response (B) | Returns the write transaction response |
| Read Address (AR) | Transfers the read address |
| Read Data (R) | Returns read data and the read response |

### VALID/READY Handshake

The VALID/READY mechanism controls transfers between the master and slave.

- `VALID`: Indicates that the sender is presenting valid information.
- `READY`: Indicates that the receiver can accept the information.
- A transfer occurs when both VALID and READY are HIGH at the same rising edge of the clock.

## 5. RTL Modules

### 5.1 Write Address Module (`write`)

This module handles the AW-channel signals, including `AWADDR`, `AWVALID`, `AWREADY`, `ACLK`, and `ARESETN`.

The current implementation:

- Keeps `AWREADY` asserted HIGH.
- Captures `AWADDR` into an internal 32-bit register when `AWVALID` and `AWREADY` are HIGH at a rising clock edge.
- Initializes four 32-bit registers (`R1`, `R2`, `R3`, and `R4`) during reset.

The current register values are:

| Register | Initial value |
|---|---|
| R1 | `32'h0000_0001` |
| R2 | `32'h0000_0005` |
| R3 | `32'h0000_0009` |
| R4 | `32'h0000_000C` |

At this stage, the AW module captures the address but does not decode that address to update the four registers.

### 5.2 Write Data Module (`write_data`)

This module handles the write-data channel. It captures `WDATA` and `WSTRB` when `WVALID` and `WREADY` are HIGH at the rising clock edge.

### 5.3 Write Response Module (`wrt_rep`)

This module generates the write response using `BVALID` and `BRESP`, based on the `write_done` input and the `BREADY` handshake.

### 5.4 Read Module (`read`)

This module handles the read-address and read-data/response signals, including `ARADDR`, `ARVALID`, `ARREADY`, `RDATA`, `RVALID`, `RREADY`, and `RRESP`.

It selects a register value based on the supplied address and produces a read response. The current RTL initializes its own local `R1`–`R4` registers separately from those in the write module.

## 6. Tools and Technologies

- **Hardware Description Language:** Verilog HDL
- **Design and Simulation Tool:** AMD Vivado
- **Target Hardware:** Boolean FPGA development board (exact device/package to be confirmed)
- **Design Methodology:** Modular RTL design
- **Verification Method:** Testbench-based behavioral simulation

## 7. Implementation Methodology

The project follows these development stages:

1. Study the AXI4-Lite protocol and its five channels.
2. Develop individual RTL modules.
3. Create testbenches for the modules.
4. Run behavioral simulation in AMD Vivado.
5. Analyze waveforms and debug incorrect behavior.
6. Integrate the modules using a top-level design.
7. Run complete RTL simulation.
8. Synthesize and implement the integrated design.
9. Generate the FPGA bitstream.
10. Program the target board and observe the hardware output.

## 8. Simulation and Debugging

Behavioral simulation is used to examine signal transitions, clock and reset behavior, address capture, and VALID/READY handshaking.

The current AW-channel testbench applies multiple address values and checks the corresponding interface behavior.

Simulation results and waveforms will be added to this repository as debugging and verification progress.

## 9. Expected Outcomes

- Modular RTL implementation of an AXI4-Lite slave interface.
- Correct operation of the individual channel logic.
- Successful integration of the read and write paths.
- Simulation results demonstrating expected transaction behavior.
- FPGA implementation of the integrated design.
- Hardware output demonstrating register-based communication.

These outcomes will be evaluated after integration, simulation, and hardware implementation.

## 10. Project Status

**Current stage:** RTL development, behavioral simulation, and debugging.

| Activity | Status |
|---|---|
| AW-channel RTL development | Initial version completed |
| AW-channel behavioral simulation | Initial simulation completed |
| Read-channel debugging | In progress |
| Write-data and write-response debugging | Pending |
| Top-level integration | Pending |
| Complete-system simulation | Pending |
| FPGA synthesis and implementation | Pending |
| Hardware testing | Pending |

## 11. Future Scope

- Complete integration of all five AXI4-Lite channels.
- Improve register address decoding and write-data handling.
- Perform comprehensive transaction-level simulation.
- Evaluate FPGA resource utilization and timing.
- Extend the interface for additional memory-mapped registers or peripherals.

## 12. References

1. Arm AMBA AXI and ACE Protocol Specification.
2. AMD Vivado Design Suite User Guides.
3. Verilog HDL language reference and RTL design documentation.

---

**Project:** RTL Design and FPGA Implementation of an AXI4-Lite Slave Interface for AMBA-Based SoC Applications

**Language:** Verilog HDL

**Tool:** AMD Vivado
