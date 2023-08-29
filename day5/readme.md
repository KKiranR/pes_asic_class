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
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/e3336cb1-18e2-4b63-812c-9854155fe235)
##### 4.opt_check4:
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/0e888977-bc90-42d8-9da9-2338d9158bcc)
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/5222ff79-e6b8-4fe8-af62-223b6f547440)
##### 5.Multiple_module_opt:
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/8cd802be-b0fc-4397-b94c-58d1a18e7163)![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/b8257532-8e2e-4a17-8cee-249ecfd641f7)

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
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/0fbc118a-15ab-42d7-aaca-f14570ef3a7c)
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/e79c3336-097a-45e6-8666-eb0aa596259b)
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/12b3f351-94ad-42a4-8df0-67342d58b573)
##### 2.dff_const2:
##### Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/6863b897-21df-4461-a0b9-d3069acc88ca)
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/ae76b1cd-a17b-4b04-b38f-35de34e2d4c1)
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/27b66e4d-bf0a-4fff-9925-30151d8a9e73)
##### 3.dff_const3:
##### Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/4edb1eae-09f3-4172-a30f-a89743d091a6)
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/c5da2445-0577-4c92-a109-2c5d305403b6)
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/d8de1377-747f-4ab4-a897-abca69c1498f)
##### 4.dff_const4:
##### Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/01cf43da-85bf-4e4e-be0c-bdceac2c1e69)
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/4234610f-dd14-4e77-89a8-610e02ea5e01)
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/eae0e928-086e-43c3-8c7b-f3c0b6728dfb)
##### 5.dff_const5:
##### Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/a92cd8dd-a861-429e-9d63-a5207f47bfc5)
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/b3bda761-8e97-4508-9d1f-2af723812f01)
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/9eab585e-424e-426d-b188-1831428def60)
### Sequential Optimization for unused outputs
##### 1.counter_opt:
##### Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/a85d4d9e-5562-4396-8ab6-c4759c23cc08)
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/7eb13951-4568-40b1-913c-1e03793d4648)
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/45c20396-7ed8-4919-8442-003610d5877c)

##### 2.counter_opt1:
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/285ad29e-8b5e-40f1-af8c-2aa1856593f1)
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/6fb7b28d-9632-41fa-be8c-be3e44fce2e1)





