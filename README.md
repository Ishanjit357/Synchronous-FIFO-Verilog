# Synchronous FIFO Design using Verilog HDL

## Overview

This project implements a synchronous First-In, First-Out (FIFO) buffer using Verilog HDL. A FIFO temporarily stores data so that it can be read in the same order in which it was written.

The design uses a single clock for both read and write operations. It includes status flags to indicate when the FIFO is full or empty, along with a counter to track the number of stored entries.

## Features

- Synchronous FIFO architecture
- Parameterized data width and FIFO depth
- Write and read enable controls
- Full and empty status flags
- Data count tracking
- Synchronous active-high reset
- Protection against writes when full and reads when empty
- Verilog testbench for functional verification
- FIFO ordering checks

## Tools and Technologies

- **HDL:** Verilog
- **Design and Simulation:** AMD Vivado
- **Verification:** Verilog testbench
- **Target FPGA:** [Add your FPGA board, if applicable]

## Project Structure

```text
Synchronous-FIFO-Verilog/
├── sync_fifo.v
├── tb_sync_fifo.v
└── README.md
```

## Design Specifications

| Parameter | Description |
|---|---|
| Data width | 8 bits |
| FIFO depth | 16 entries |
| Total storage capacity | 128 bits |
| Clock | Single synchronous clock |
| Reset | Synchronous, active-high |
| Output | Registered data output |
| Status flags | `full` and `empty` |
| Occupancy indicator | `count` |

The FIFO depth is assumed to be a power of two in the current design.

## Block Diagram

```text
          +----------------------+
  clk --->|                      |
 reset -->|                      |
  wr_en ->|                      |
  rd_en ->|     Synchronous      |
 data_in >|         FIFO         |----> data_out
          |                      |
          |                      |----> full
          |                      |----> empty
          |                      |----> count
          +----------------------+
```

## Working Principle

1. **Write operation:** When `wr_en` is asserted and the FIFO is not full, the input data is stored in memory.
2. **Read operation:** When `rd_en` is asserted and the FIFO is not empty, the next available data is read.
3. **Full condition:** The `full` flag indicates that all FIFO entries are occupied.
4. **Empty condition:** The `empty` flag indicates that no valid entries are available to read.
5. **Count tracking:** The `count` output indicates the number of stored entries.
6. **Reset:** The synchronous active-high reset initializes the FIFO state.

A write request while full and a read request while empty are ignored. If simultaneous read and write requests occur, the design behavior depends on the current FIFO status and the RTL implementation.

## Testbench and Verification

The testbench is designed to verify the following scenarios:

- Reset initialization
- Writing data until the FIFO becomes full
- Checking the full flag
- Attempting a write when full
- Reading data and checking FIFO ordering
- Reading until the FIFO becomes empty
- Attempting a read when empty
- Checking occupancy count and status flags

**Simulation status:** [Update after running the testbench in Vivado.]

## How to Run in Vivado

1. Open AMD Vivado and create a new RTL project.
2. Add `sync_fifo.v` as a design source.
3. Add `tb_sync_fifo.v` as a simulation source.
4. Set `tb_sync_fifo` as the simulation top module.
5. Run **Behavioral Simulation**.
6. Inspect the clock, reset, read enable, write enable, input data, output data, `full`, `empty`, and `count` signals.
7. Confirm that data is read in the same order in which it was written.

## Learning Outcomes

- Understanding FIFO memory organization
- Designing read and write pointer logic
- Implementing control logic and status flags
- Handling FIFO overflow and underflow requests
- Writing Verilog testbenches
- Debugging synchronous digital designs using simulation waveforms

## Future Improvements

- Support configurable data width and depth
- Add asynchronous FIFO support for different clock domains
- Add almost-full and almost-empty flags
- Improve verification with randomized test sequences
- Implement on an FPGA development board and evaluate resource utilization

## Author

**[Your Name]**  
M.Tech, Communication and Signal Processing  
Indian Institute of Technology Indore

## License

This project is available for educational and learning purposes. Add a license file if you want to specify reuse and distribution terms.
