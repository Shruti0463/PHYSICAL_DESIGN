# PHYSICAL_DESIGN


````md
# OpenLane Physical Design – PicoRV32A

This project demonstrates the **RTL-to-GDSII ASIC physical design flow** using the **PicoRV32A RISC-V processor**, **OpenLane**, and the **Sky130 PDK**.

The project covers the major stages of digital ASIC implementation, starting from RTL and progressing through synthesis, floorplanning, power planning, placement, clock tree synthesis, routing, timing analysis, physical verification, and GDSII generation.

---

## 1. Project Overview

ASIC physical design converts a digital circuit described using RTL into a physical layout suitable for semiconductor fabrication.

In this project, **PicoRV32A** is used as the design to demonstrate the complete physical implementation process.

### Physical Design Flow

```text
RTL
 ↓
Synthesis
 ↓
Floorplanning
 ↓
Power Planning
 ↓
Placement
 ↓
Clock Tree Synthesis
 ↓
Routing
 ↓
Static Timing Analysis
 ↓
Physical Verification
 ↓
GDSII
````

<img width="1246" height="487" alt="image" src="https://github.com/user-attachments/assets/6e4d5be5-ea6e-46e8-811d-4ea6e1526754" />


---

## 2. PicoRV32A

**PicoRV32A** is a compact RISC-V processor core described using Verilog RTL.

The RTL represents the logical behavior and structure of the processor before physical implementation.

The design consists of various digital components, including:

* Registers
* Flip-flops
* Multiplexers
* Arithmetic logic
* Control logic
* Instruction decoding logic
* Combinational logic

The RTL description is provided as the input to the synthesis stage.

---

## 3. Process Design Kit – Sky130

**PDK stands for Process Design Kit.**

A PDK contains the technology-specific information required by EDA tools to implement a digital circuit.

The Sky130 PDK provides information such as:

* Standard-cell libraries
* Technology layers
* Design rules
* Timing models
* Physical cell information
* Layout information

This project uses the **Sky130 open-source process technology** for technology mapping and physical implementation.

---

## 4. OpenLane

**OpenLane** is an open-source RTL-to-GDSII ASIC implementation flow.

It integrates several open-source EDA tools to automate the different stages of physical design.

### OpenLane Flow

```text
RTL + PDK
   ↓
Logic Synthesis
   ↓
Floorplanning
   ↓
Power Planning
   ↓
Placement
   ↓
Clock Tree Synthesis
   ↓
Routing
   ↓
Timing Analysis
   ↓
Physical Verification
   ↓
GDSII
```

OpenLane provides an automated environment for taking an RTL design through the major stages of ASIC implementation.

---

## 5. RTL and Synthesis

**RTL stands for Register Transfer Level.**

RTL describes the behavior and data movement of a digital circuit.

The first major implementation step is **logic synthesis**, where the RTL is converted into a gate-level representation.

```text
RTL
 ↓
Logic Synthesis
 ↓
Gate-Level Netlist
```

The synthesis process maps the logical design to cells available in the selected technology library.

The resulting netlist can contain:

* AND gates
* OR gates
* NAND gates
* NOR gates
* Inverters
* Buffers
* Multiplexers
* Flip-flops

### Synthesis Result

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9a2dc589-d84e-455d-a769-f1c54a6a9190" />


---

## 6. Gate-Level Netlist

A **netlist** represents the cells present in the synthesized design and the connections between those cells.

During synthesis, the original RTL description is transformed into a technology-mapped gate-level netlist.

```text
RTL
 ↓
Logic Synthesis
 ↓
Standard Cells
 ↓
Cell Connections
 ↓
Gate-Level Netlist
```

The netlist becomes the logical input for the subsequent physical-design stages.

### Generated Netlist

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ebf43fb8-c32b-491f-9eea-2ff2a164eb77" />


---

## 7. Floorplanning

**Floorplanning** establishes the initial physical organization of the chip.

During floorplanning, important physical parameters such as the following are determined:

* Die dimensions
* Core dimensions
* Core utilization
* I/O locations
* Placement boundaries
* Available routing area

A well-planned floorplan helps achieve better placement, routing, timing, and area utilization.

---

## 8. Power Planning

**Power planning** creates the power distribution network required to supply the standard cells.

The power network generally contains:

* VDD
* VSS
* Power rings
* Power straps
* Power rails

The purpose of the power distribution network is to provide reliable power and ground connections throughout the design.

```text
VDD / VSS
    ↓
Power Network
    ↓
Power Straps
    ↓
Standard Cell Rails
    ↓
Standard Cells
```

---

## 9. Placement

**Placement** determines the physical locations of standard cells inside the core area.

The placement process is generally divided into two stages.

### Global Placement

Global placement determines approximate positions for the cells while considering:

* Cell density
* Timing
* Wire length
* Routing congestion

### Detailed Placement

Detailed placement adjusts the cells to legal locations according to the placement rules.

Effective placement helps to:

* Reduce interconnect length
* Reduce congestion
* Improve timing
* Improve area utilization
* Simplify routing

---

## 10. Clock Tree Synthesis

**CTS stands for Clock Tree Synthesis.**

Clock Tree Synthesis creates a clock distribution network that connects the clock source to sequential elements such as flip-flops.

Clock buffers may be inserted to control clock delay and improve clock distribution.

```text
          Clock
            |
          Buffer
        /   |   \
    Buffer Buffer Buffer
      |      |      |
     FF1    FF2    FF3
```

### Objectives of CTS

The main objectives are:

* Control clock latency
* Reduce clock skew
* Provide balanced clock distribution
* Ensure reliable clock delivery to sequential elements

---

## 11. Routing

**Routing** establishes the physical metal connections between the placed cells.

The routing process determines how signals travel between different cells using the available metal layers.

### Global Routing

Global routing determines the general paths for the different connections.

### Detailed Routing

Detailed routing creates the actual metal and via structures while following the technology-specific design rules.

```text
Placed Cells
     ↓
Global Routing
     ↓
Detailed Routing
     ↓
Physical Interconnections
```

### RTL to GDSII Flow
<img width="1337" height="818" alt="image" src="https://github.com/user-attachments/assets/6df49211-07cf-4203-bedb-a4aa95217dab" />


---

## 12. Static Timing Analysis

**STA stands for Static Timing Analysis.**

STA is used to determine whether the implemented design satisfies its timing requirements.

The timing analysis considers parameters such as:

* Cell delay
* Net delay
* Clock delay
* Setup time
* Hold time
* Clock skew
* Slew
* Slack

### Slack

Slack represents the timing margin available on a path.

```text
Positive Slack
      ↓
Timing Requirement Satisfied

Negative Slack
      ↓
Timing Violation
```

OpenSTA can be used to perform static timing analysis within the open-source physical-design flow.

### STA Report

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0b9c9905-c3de-4db7-9a3b-6b441eb818e0" />


---

## 13. Physical Verification and Signoff

**Signoff** is the final verification stage before the physical layout is considered ready for final output.

Several checks are performed to verify the correctness of the implementation.

### DRC

**Design Rule Check**

DRC verifies that the physical layout follows the manufacturing rules specified by the technology.

It can check parameters such as:

* Metal width
* Metal spacing
* Via dimensions
* Layer spacing
* Geometrical constraints

### LVS

**Layout Versus Schematic**

LVS compares the extracted layout connectivity with the intended circuit/netlist.

The purpose is to ensure that the physical implementation represents the correct logical design.

### Timing Verification

Timing analysis is also performed to determine whether the design satisfies the required timing constraints.

After successful physical verification and signoff, the final layout can be exported in **GDSII** format.

---

## 14. OpenLane Commands

The OpenLane environment can be started using:

```bash
./flow.tcl -interactive
```

Inside the OpenLane environment, the design can be prepared using the appropriate commands for the installed OpenLane version.

For example:

```tcl
package require openlane 0.9
prep -design picorv32a
```

The synthesis and subsequent physical-design stages can then be executed according to the OpenLane version and configuration being used.

> **Note:** OpenLane command syntax can vary between different releases. Therefore, commands should always match the version installed in the VSDIAT environment.

---

## 15. Project Results

The OpenLane flow produces several intermediate and final results during implementation.

These results can include:

* Synthesized netlist
* Floorplan
* Placement database
* Clock tree
* Routed design
* Timing reports
* Physical verification reports
* GDSII layout

### Design Statistics

<img width="451" height="742" alt="image" src="https://github.com/user-attachments/assets/5bddbf93-885f-40d7-a2fe-f7cacd57d377" />


---

## 16. Synthesis Statistics

The recorded PicoRV32A synthesis results are:

| Parameter        |  Value |
| ---------------- | -----: |
| Total Wires      | 14,596 |
| Wire Bits        | 14,978 |
| Public Wires     |  1,565 |
| Public Wire Bits |  1,947 |
| Memories         |      0 |
| Processes        |      0 |
| Total Cells      | 14,876 |
| Flip-Flops       |  1,613 |

These values provide an overview of the logical complexity of the synthesized design.

---

## 17. Flip-Flop Ratio

The **flip-flop ratio** indicates the percentage of the total synthesized cells that are flip-flops.

### Formula

```text
Flip-Flop Ratio =
(Flip-Flops / Total Cells) × 100
```

For the recorded synthesis results:

```text
Flip-Flops = 1613
Total Cells = 14876
```

Therefore:

```text
(1613 / 14876) × 100
= 10.84%
```

Hence:

**Flip-Flop Ratio ≈ 10.84%**

---

## 18. Complete Physical Design Flow

The complete implementation process can be represented as:

```text
RTL
 ↓
Logic Synthesis
 ↓
Gate-Level Netlist
 ↓
Floorplanning
 ↓
Power Planning
 ↓
Placement
 ↓
Clock Tree Synthesis
 ↓
Routing
 ↓
Static Timing Analysis
 ↓
Physical Verification
 ↓
Signoff
 ↓
GDSII
```

Each stage transforms the design into a more physically detailed representation.

---

## 19. Tools Used

| Tool / Technology | Purpose                          |
| ----------------- | -------------------------------- |
| PicoRV32A         | RISC-V processor RTL             |
| OpenLane          | RTL-to-GDSII implementation flow |
| Yosys             | Logic synthesis                  |
| OpenROAD          | Physical implementation          |
| OpenSTA           | Static timing analysis           |
| Sky130            | Process technology and PDK       |
| Magic             | Layout and physical verification |
| Netgen            | LVS verification                 |
| GDSII             | Final physical layout format     |

---

## 20. What I Learned

This project provided practical exposure to the **ASIC physical design flow** using open-source EDA tools.

The major concepts covered include:

* RTL design
* RISC-V processor
* Process Design Kit
* Logic synthesis
* Gate-level netlist
* Standard cells
* Floorplanning
* Power planning
* Placement
* Clock Tree Synthesis
* Global routing
* Detailed routing
* Static Timing Analysis
* Setup and hold analysis
* Slack
* Design Rule Check
* Layout Versus Schematic
* Physical verification
* Signoff
* GDSII generation

The overall transformation can be summarized as:

```text
RTL
 ↓
Netlist
 ↓
Physical Implementation
 ↓
Timing Analysis
 ↓
Physical Verification
 ↓
Signoff
 ↓
GDSII
```

---

## 21. Conclusion

The **PicoRV32A OpenLane project** demonstrates how a RISC-V processor described using Verilog RTL can be taken through the major stages of ASIC physical design.

Starting from RTL, the design is synthesized into a gate-level netlist and then physically implemented through floorplanning, power planning, placement, CTS, and routing.

Timing analysis and physical verification are performed before the final layout is generated.

The project provides practical understanding of the relationship between **RTL design, synthesis, physical implementation, verification, and final GDSII generation** using open-source tools and the **Sky130 technology**.

### Final Flow

```text
RTL
 ↓
Synthesis
 ↓
Netlist
 ↓
Floorplanning
 ↓
Power Planning
 ↓
Placement
 ↓
CTS
 ↓
Routing
 ↓
STA
 ↓
Physical Verification
 ↓
Signoff
 ↓
GDSII
```

```
```
