# Day 5
### Introduction to Optimizations
#### Combinational Optimizations:
- combinational logic refers to logic circuits where the outputs depend only on the current inputs and not on any previous states.
- Combinational optimization is a field of study in computer science and operations research that focuses on finding the best possible solution from a finite set of options for problems that involve discrete variables and have no inherent notion of time.
- Optimising the combinational logic circuit is squeezing the logic to get the most optimized digital design so that the circuit finally is area and power efficient.
- ##### Techniques for Optimizations:
  - **Constant propagation** is an optimization technique used in compiler design and digital circuit synthesis to improve the efficiency of code and circuit implementations by replacing variables or expressions with their constant values where applicable.
  - **Boolean logic optimization**, also known as logic minimization or Boolean function simplification, is a process in digital design that aims to simplify Boolean expressions or logic circuits by reducing the number of terms, literals, and gates required to implement a given logical function.
#### Sequential Logic Optimizations
- Sequential logic optimizations involve improving the efficiency, performance, and resource utilization of digital circuits that include memory elements like flip-flops and latches.
- Optimizing sequential logic is crucial in ensuring that digital circuits meet timing requirements, consume minimal power, and occupy the least possible area while maintaining correct functionality.
- ##### Techniques for Optimizations:
  - **Sequential constant propagation**, also known as constant propagation across sequential elements, is an optimization technique used in digital design to identify and propagate constant values through sequential logic elements like flip-flops and registers. This technique aims to replace variable values with their known constant values at various stages of the logic circuit, optimizing the design for better performance and resource utilization.
  - **State optimization**, also known as state minimization or state reduction, is an optimization technique used in digital design to reduce the number of states in finite state machines (FSMs) while preserving the original functionality.
  - **Sequential logic cloning**, also known as retiming-based cloning or register cloning, is a technique used in digital design to improve the performance of a circuit by duplicating or cloning existing registers (flip-flops) and introducing additional pipeline stages. This technique aims to balance the critical paths within a circuit and reduce its overall clock period, leading to improved timing performance and better overall efficiency.
  - **Retiming** is an optimization technique used in digital design to improve the performance of a circuit by repositioning registers (flip-flops) along its paths to balance the timing and reduce the critical path delay. The primary goal of retiming is to achieve a shorter clock period without changing the functionality of the circuit.
## Lab
### Combinational Logic Optimizations
- **All the files are present in the verilog_files directory from the folder sky130RTLDesignAndSynthesisWorkshop**
#### Commmands to run the Yosys 
``` bash=
gedit <file name > # this will give you the code for the file specified
yosys # this will open the yosys synthesis tool
read_liberty -lib <library file name > # this will read the library file name
read_verilog <file name > # this will read the verilog file name
synth -top <top module name > # this will synthesize the top module
opt_clean -purge
abc -liberty <library file name >
show
```
##### 1.opt_check:
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/1788c767-af26-473b-bfc8-2d5fa1836596)
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/642fd96c-5a00-490e-bf41-98c8573c7419)
##### 2.opt_check2:
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/e8f94de8-1fe2-4146-9ac2-6458d67fcf00)
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/1d5cdf5e-6155-41bd-959f-e4e02ae7b914)
##### 3.opt_check3:
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/f0f2fe7e-17c5-4522-802c-e66d59764e37)
![](https://hackmd.io/_uploads/SJorFIs62.png)
##### 4.opt_check4:
![image](https://hackmd.io/_uploads/HJ-cqIipn.png)
![](https://hackmd.io/_uploads/SyQ2cLi6n.png)
##### 5.Multiple_module_opt:
![](https://hackmd.io/_uploads/BJwqi8sph.png)![](https://hackmd.io/_uploads/B13x28oa3.png)
### Sequential Optimizations
#### Commands to simulation and synthesis 
```bash=
###*****For Simulation*****###
iverilog <design_file > <test_bench_file > 
./a.out
gtkwave <.vcd_file >
###*****For Synthesis*****###
yosys
read_liberty -lib <libraryfile>
read_verilog <design_file>
synth -top <top_module>
dfflibmap -liberty <library_file>
abc -liberty <library_file>
show
```
##### 1.dff_const1:
##### Simulation
![](https://hackmd.io/_uploads/rJTCTUi63.png)
##### Synthesis
![](https://hackmd.io/_uploads/r1c76Usph.png)
![](https://hackmd.io/_uploads/BkZGpUs6n.png)
##### 2.dff_const2:
##### Simulation
![](https://hackmd.io/_uploads/HJWUgDian.png)
##### Synthesis
![](https://hackmd.io/_uploads/H1Negwsp2.png)
![](https://hackmd.io/_uploads/SJmMgvja3.png)
##### 3.dff_const3:
##### Simulation
![](https://hackmd.io/_uploads/Skgoews6n.png)
##### Synthesis
![](https://hackmd.io/_uploads/HkhpePian.png)
![](https://hackmd.io/_uploads/rks1ZPs63.png)
##### 4.dff_const4:
##### Simulation
![](https://hackmd.io/_uploads/Hkb4WDian.png)
##### Synthesis
![](https://hackmd.io/_uploads/ByVLZvoah.png)
![](https://hackmd.io/_uploads/ByU_Zwoa2.png)
##### 5.dff_const5:
##### Simulation
![](https://hackmd.io/_uploads/H1Nzzvja2.png)
##### Synthesis
![](https://hackmd.io/_uploads/HyaYzws63.png)
![](https://hackmd.io/_uploads/S1epfPiT2.png)
### Sequential Optimization for unused outputs
##### 1.counter_opt:
##### Simulation
![](https://hackmd.io/_uploads/rJAeIDja3.png)
##### Synthesis
![](https://hackmd.io/_uploads/B17GBPja3.png)
![](https://hackmd.io/_uploads/Hkp5SPjah.png)
##### 2.counter_opt1:
##### Synthesis
![](https://hackmd.io/_uploads/rkYp8Dia3.png)
![](https://hackmd.io/_uploads/rk1gPDop2.png)




