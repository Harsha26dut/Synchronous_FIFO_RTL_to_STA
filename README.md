# ⚡️ Synchronous FIFO (First-In, First-Out) RTL-to-STA Flow

## 📖 Overview

This repository documents the complete **Register Transfer Level (RTL) to Static Timing Analysis (STA)** implementation flow for a generic synchronous First-In, First-Out (FIFO) buffer. The project uses open-source tools—**SystemVerilog** for design and verification, **Yosys** for logic synthesis, and **OpenSTA** for timing verification—demonstrating a complete and reproducible ASIC/FPGA design flow.

**Key Features:**
* Synchronous read and write operations.
* Generation of `full` and `empty` status flags.
* Parameterized width and depth (currently set for X-bit wide, Y-deep).

## 🗂️ Repository Structure

| Directory/File | Description |
| :--- | :--- |
| `rtl/` | Contains the source SystemVerilog RTL code (`fifo.sv`). |
| `tb/` | Contains the SystemVerilog Testbench (`fifo_tb.sv`) for verification. |
| `synthesis/` | Contains Yosys synthesis scripts/commands and the resulting netlist. |
| `sta/` | Contains the timing constraints (`constraints.sdc`) and the OpenSTA analysis scripts and reports. |
| `EDAplayground_link.txt` | Direct link to the working simulation environment. |
| `README.md` | This document. |

## 🛠️ Implementation Flow & Tools

The design was carried out using the following open-source toolchain:

1.  **RTL Design & Verification:**
    * **Language:** SystemVerilog
    * **Simulation Environment:** EDAplayground
    * **Link:** https://www.edaplayground.com/x/s7kR

2.  **Logic Synthesis (RTL to Netlist):**
    * **Tool:** Yosys Open-Source Synthesis Suite
    * **Implementation Environment:** Windows Subsystem for Linux (WSL)
    * **See:** [`synthesis/synthesis_commands.txt`](synthesis/synthesis_commands.txt) for the exact synthesis steps.

3.  **Static Timing Analysis (STA):**
    * **Tool:** OpenSTA (Open-Source Static Timing Analyzer)
    * **Goal:** Verify that the netlist meets the specified timing constraints, calculating setup and hold slacks.
    * **Constraints:** Defined in [`sta/constraints.sdc`](sta/constraints.sdc).
    * **See:** [`sta/sta_commands.txt`](sta/sta_commands.txt) for the OpenSTA script and [`sta/report_timing.txt`](sta/report_timing.txt) for the final timing report.

## ⚙️ How to Replicate the Synthesis and STA

### 1. Prerequisites

You must have the following tools installed and accessible on your path (preferably in a Linux environment like WSL or Docker):
* Yosys
* OpenSTA
* A Standard Cell Library (e.g., sky130 or any library used for your analysis). *Note: The timing analysis here assumes a basic/generic library for demonstration.*

### 2. Synthesis

Run the commands found in [`synthesis/synthesis_commands.txt`](synthesis/synthesis_commands.txt) in your terminal to generate the technology-mapped netlist.

```bash
# Example Yosys commands used:
yosys -p "read_verilog rtl/fifo.sv; synth -top fifo; write_verilog synthesis/fifo_netlist.v"

### 3. Static Timing Analysis

# Example OpenSTA command:
# Run the TCL script that executes the full STA flow.
sta sta/commands.tcl
