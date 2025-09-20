# Task 2: Tool Installation

This task covers the installation of all essential tools required for the **RISC-V SoC Tapeout Program**.  
The tools include **Yosys, Icarus Verilog, GTKWave, Ngspice, Magic, and OpenLANE**.  

---

## System Requirements
- **OS**: Ubuntu 20.04+  
- **RAM**: 6 GB minimum  
- **Disk**: 50 GB free space  
- **CPU**: 4 vCPU  
- **Virtualization**: [Oracle VirtualBox Download]

---
 
- **Why Linux?** Most open-source EDA/ASIC tools are built for Linux. Ubuntu provides **package management, scripting, and permission control** that are essential for installing, running, and automating these tools.

---

## 1. Yosys
**What it is:** Open-source Verilog synthesis tool.  
**Purpose:** Converts RTL designs into gate-level netlists for ASIC flow.  
**Installation commands:**
```bash
git clone https://github.com/YosysHQ/yosys.git
cd yosys
make config-gcc
make
sudo make install
````

**Interrelation:** Used by OpenLane as the first step in synthesis. RTL designs are first verified in Iverilog/GTKWave and then synthesized by Yosys.

---

## 2. Iverilog

**What it is:** Open-source Verilog compiler and simulator.
**Purpose:** Simulates RTL designs for functional verification before synthesis.
**Installation commands:**

```bash
sudo apt-get update
sudo apt-get install iverilog
```

**Interrelation:** Generates VCD waveform files that can be visualized with GTKWave.

---

## 3. GTKWave

**What it is:** Waveform viewer for VCD/FSDB files.
**Purpose:** Visualizes signal changes from RTL simulation to verify correctness.
**Installation commands:**

```bash
sudo apt-get update
sudo apt install gtkwave
```

**Interrelation:** Works directly with Iverilog simulation output.

---

## 4. ngspice

**What it is:** Open-source SPICE simulator for analog/mixed-signal circuits.
**Purpose:** Simulates transistor-level behavior of standard cells.
**Installation commands:**

```bash
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release && cd release
../configure --with-x --with-readline=yes --disable-debug
make
sudo make install
```

**Interrelation:** Used with Magic for LVS/DRC checks or analog verification of cells.

---

## 5. Magic

**What it is:** VLSI layout editor.
**Purpose:** Designs and verifies the physical layout of ICs.
**Installation commands:**

```bash
git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
make
sudo make install
```

**Interrelation:** Works with OpenLane to perform **DRC (Design Rule Check) / LVS (Layout vs Schematic)**. Can interact with ngspice for analog simulations.

---

## 6. OpenLane

**What it is:** Full digital ASIC flow automation tool.
**Purpose:** Automates synthesis, placement, routing, and verification to generate GDSII layout.
**Installation commands:**

```bash
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make pdk   # Downloads Sky130 PDK
make test  # Runs demo spm design
```

**Interrelation:** Integrates all above tools — Yosys (synthesis), Magic (layout), ngspice (optional analog checks), Iverilog/GTKWave (RTL verification). Requires Sky130 PDK.

---

## Interrelation Overview

| Step                 | Tool(s)            | Purpose                                                  |
| -------------------- | ------------------ | -------------------------------------------------------- |
| RTL verification     | Iverilog + GTKWave | Ensures RTL behaves correctly before synthesis           |
| Synthesis            | Yosys              | Converts RTL to netlist for placement & routing          |
| Layout & checks      | Magic + ngspice    | DRC, LVS, analog simulation                              |
| Full flow automation | OpenLane           | Automates end-to-end ASIC design using all tools and PDK |

---

**Notes:**

* Always run `make pdk` **without sudo** to avoid permission issues.
*Snapshots of the installed tools and dependencies are given in [task_2installation_images]
* Ubuntu/Linux is essential because these open-source tools rely on Linux utilities, shell scripting, and proper file permissions.

```

---



