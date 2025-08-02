# tinyXPU
A tiny, eXtensible FPGA-based coprocessor framework that accelerates compute-heavy tasks on microcontrollers.

---

## Overview

**tinyXPU** is a lightweight, reconfigurable hardware coprocessor framework designed to work alongside low-power microcontrollers, such as ARM Cortex-M series. Built on an FPGA and controlled via SPI, it enables offloading of tasks that are too slow or compute-intensive for the MCU alone.

The project includes a Verilog-based implementation of a basic SPI slave interface, command decoder, and several simple compute modules (e.g., FFT, matrix multiplication). On the microcontroller side, a C++ simulation of an SPI master communicates with the FPGA to send commands and receive results.

**tinyXPU** is simulation-ready using Verilator and is intended as a base for further development into a full hardware-accelerated co-processing unit.

---

## What is an XPU?

An XPU (more like an **[X]PU**) is an **eXtensible**, **fleXible**, and **reconfiXurable** co-processing unit. It's built to help microcontrollers accelerate specific workloads that would otherwise be too demanding or inefficient to run in software.

### Typical tasks offloaded to an XPU:
- Parallel data processing  
- Graphics or signal processing  
- Lightweight machine learning inference  
- Any custom logic that doesn’t fit well in software

Unlike fixed-function units like GPUs or TPUs, an XPU is **application-specific** and fully customizable using Verilog. The “X” can stand for **eXtension**, **fleXibility**, **eXecution**, or **eXperimentation** — it’s up to you.

---

## Why Use an XPU with an MCU?

Microcontrollers are great at controlling hardware and handling I/O, but they’re not built for high-throughput computation. XPUs fill this gap by acting as task-specific hardware accelerators. Instead of upgrading to a more powerful (and power-hungry) processor, you can pair your MCU with an FPGA to handle the heavy lifting.

This approach is especially useful in:
- Low-power embedded systems  
- Projects needing real-time processing  
- Scenarios where deterministic timing is essential  
- Prototyping of custom instruction sets or compute units  

---

## How It Works

The microcontroller (or simulated MCU) acts as the **SPI master**, sending commands and raw data to the FPGA. The FPGA implements an **SPI slave** that receives this data, decodes the command, and dispatches it to the appropriate module.

### Example flow:
1. MCU sends a command over SPI (e.g., “run FFT on this buffer”).
2. FPGA command decoder routes the request to the `xpu_fft` module.
3. The result is sent back to the MCU over SPI or output through a UART for debugging.

Each accelerator module is written in Verilog and connected through a simple internal bus or control path. The architecture is modular, so new compute blocks can be added easily.

---

## Project Structure

This version of tinyXPU is simulation-ready and includes basic compute modules. It is primarily intended for experimentation and learning around:

- MCU–FPGA communication over SPI  
- Verilog module design and testing  
- Hardware-software co-design  
- Embedded acceleration architectures
```
