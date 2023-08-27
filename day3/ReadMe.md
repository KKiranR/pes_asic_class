# Day 3
## Introduction to Open Source Simulator Iverilog
**Simulator**: RTL design is checked for adherence to the spec by simulating the design. Simulator is the tool used for simulating the design

**Design**: Design is the actual verilog codeor set of verilog codes which has the intended functionality to meet with the required specification

**Testbench**: Testbench is the setup to apply stimulus to the design to check its functionality
### How do simulator works ?
Simulator flows are mentioned below with screen shots as it take the inputs from the testbench and connects it to the source file and gives you a file in format .vcd this file is used to run the wave forms in the GTK wave software 

![Screenshot from 2023-08-27 11-26-25](https://github.com/KKiranR/pes_asic_class/assets/89727621/95a51807-9085-43af-a8d2-99994c1cfd56)

### Simulation of Mux:
Run the following commands to simulate mux
``` bash
iverilog mux.v mux_tb.v
./a.out
gtkwave tb_good_mux.vcd
```
after the command ```./a.out``` .vcd file will be created and used for the simulation 

![Screenshot from 2023-08-27 11-37-27](https://github.com/KKiranR/pes_asic_class/assets/89727621/1a954eb7-8128-4e35-8fc3-28bf7771822e)

#### Output:
![Screenshot from 2023-08-27 11-37-46](https://github.com/KKiranR/pes_asic_class/assets/89727621/bced5eb3-1873-4134-8304-9542a944ba90)

### Intrduction to Yoyo sys
Yosys is an synthesizer which is used to convert RTL to netlist

![Screenshot from 2023-08-27 14-09-45](https://github.com/KKiranR/pes_asic_class/assets/89727621/a0da34af-0739-4365-b2fe-c2a8b376f36a)

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

**Tick Formula:**![263467104-4737db4a-c1db-47a3-8c6b-1c8634c00189](https://github.com/KKiranR/pes_asic_class/assets/89727621/b86eb254-5f71-4533-823e-1ae3dfc85877)

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
![Screenshot from 2023-08-27 14-31-45](https://github.com/KKiranR/pes_asic_class/assets/89727621/c1ec8177-ca0e-4174-bd3b-a9dfc1a68f7e)
![Screenshot from 2023-08-27 14-33-04](https://github.com/KKiranR/pes_asic_class/assets/89727621/954184c7-831a-4176-96f5-01541288afaa)
![Screenshot from 2023-08-27 14-34-05](https://github.com/KKiranR/pes_asic_class/assets/89727621/44ef39b3-ea90-4a4b-9c63-66fb388cfa9c)
![Screenshot from 2023-08-27 14-34-25](https://github.com/KKiranR/pes_asic_class/assets/89727621/64580477-e473-492d-9b02-e8aa682646a2)
![Screenshot from 2023-08-27 14-34-44](https://github.com/KKiranR/pes_asic_class/assets/89727621/42972a85-aa4d-4f44-8f14-7b6b318c9b54)




