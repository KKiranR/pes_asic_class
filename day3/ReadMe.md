# Day 3
## Introduction to Open Source Simulator Iverilog
**Simulator**: RTL design is checked for adherence to the spec by simulating the design. Simulator is the tool used for simulating the design

**Design**: Design is the actual verilog codeor set of verilog codes which has the intended functionality to meet with the required specification

**Testbench**: Testbench is the setup to apply stimulus to the design to check its functionality
### How do simulator works ?
Simulator flows are mentioned below with screen shots as it take the inputs from the testbench and connects it to the source file and gives you a file in format .vcd this file is used to run the wave forms in the GTK wave software 

![](https://hackmd.io/_uploads/HymyDPda3.png)
### Simulation of Mux:
Run the following commands to simulate mux
``` bash
iverilog mux.v mux_tb.v
./a.out
gtkwave tb_good_mux.vcd
```
after the command ```./a.out``` .vcd file will be created and used for the simulation 

![](https://hackmd.io/_uploads/rJqXODu63.png)
#### Output:
![](https://hackmd.io/_uploads/B1DBODOpn.png)
### Intrduction to Yoyo sys
Yosys is an synthesizer which is used to convert RTL to netlist

![](https://hackmd.io/_uploads/SJzGnYu6h.png)
**`netlist` is the representation of `DESIGN` in the form of standard cells present in `.lib`**

- To verify synthesis Netlist need to be fed to iverilog along with testbench
- vcd file generated from iverilog need to be fed to gtkwave simulator
- The output we get should be same as the output we got during RTL simulator
### Introduction to Logical Synthesis
Logic synthesis is a vital step in digital circuit design where high-level descriptions of circuits are transformed into specific implementations using logic gates. It optimizes circuits for factors like performance, area, power, and cost. The process includes library mapping, optimization, technology mapping, timing analysis, and verification. It's an iterative process often done with specialized software tools, enabling efficient hardware design.

**.lib:**
- Logic synthesis tools use a library of standard cells.
-  These cells are predefined logic gates with different functionalities and characteristics
-  It will also contain fast and slow version of same gate
#### why fast and slow version of same gate?
Fast and slow versions of gates are essential in digital circuit design to balance between clock frequency and timing constraints. Fast gates have shorter propagation delays and are used to reduce setup and hold time violations, allowing for higher clock frequencies. Slow gates, with longer delays, can be used to intentionally slow down critical paths or address timing issues. The Tclk formula helps calculate the maximum clock frequency while considering these factors

**Tick Formula:**![](https://hackmd.io/_uploads/HyhGTKdan.png)
- **t_setup:** The setup time is the minimum time before the clock edge when the input data must be stable.
- **t_hold:** The hold time is the minimum time after the clock edge during which the input data must remain stable.
- **t_propagation:** This term represents the propagation delay of the logic gates in the critical path.
- **Tcq:** This term represents the clock-to-q delay of the flip-flops or registers used in the design. It's often a fixed value based on the chosen flip-flop technology.
## Lab
Steps to realize good_mux(design) in terms of standard cells avilable in library sky130_fd_sc_hd__tt_025C_1v80.lib
- **Step-1:** Go to the location of the where the verilog files and type command ```yosys``` in the terminal
- **Step-2:** Read Library ```read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib``` 
- **Step-3:** Read the design File ```read_verilog good_mux.v```
- **Step-4:** Do the synthesis using command ``` synth -top good_mux```
- **Step-5:** Generate netlist using command ``` abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib```
- **Step-6:** To get the schematic run command ```show```
- **Step-7:** Write the netlist using command ```write_verilog -noattr good_mux_netlist.v```,```!gvim good_mux_netlist.v```
### Output:
![](https://hackmd.io/_uploads/rkFwZcuT2.png)
![](https://hackmd.io/_uploads/BJlq-cOp2.png)
![](https://hackmd.io/_uploads/HyNo-5_a2.png)
![](https://hackmd.io/_uploads/SkF6bq_Th.png)
![](https://hackmd.io/_uploads/ryUhWcOpn.png)




