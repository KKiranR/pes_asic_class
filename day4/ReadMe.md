# Day4
## Introduction to timing dot libs
### sky130_fd_sc_hd__tt_025C_1v80.lib
- **sky130:** This indicates that the library is associated with the SkyWater 130nm process technology. Process technology refers to the manufacturing process used to create integrated circuits (ICs) and determines factors like transistor size and performance characteristics.
- **fd_sc_hd:** These letters likely stand for different aspects of the library. "fd" might refer to "Foundation," suggesting that this library contains fundamental building blocks for digital IC design. "sc" could stand for "Standard Cells," which are pre-designed logic gates used in IC design. "hd" could refer to "high-density" libraries, which typically contain smaller, more compact cell designs for achieving higher logic density in ICs.
- **tt_025C:** This part of the name could refer to the library's operating conditions or temperature and voltage settings. "tt" might stand for "typical temperature," and "025C" could refer to 25 degrees Celsius, a common temperature for IC specifications. These conditions are important for characterizing the library's performance.
- **1v80:** This likely represents the supply voltage for the library. In this case, "1v80" indicates a supply voltage of 1.8 volts, which is a common voltage level for digital ICs.
### Libraries Contains
- **Standard Cells:** This library is likely to include a variety of standard cells, which are pre-designed building blocks for digital logic. Standard cells consist of logic gates (e.g., AND, OR, XOR), flip-flops, latches, multiplexers, and other fundamental digital components. These cells are characterized for the specific process technology (in this case, SkyWater 130nm) and operating conditions (temperature and voltage).
- **Timing Information:** The library will provide timing information for each standard cell. This information includes parameters like propagation delay, setup time, hold time, and other timing characteristics. Designers use this data to ensure that signals propagate correctly through the logic gates.
- **Power Characteristics:** Power consumption data is crucial for estimating the energy usage of a design. The library will typically include information on dynamic power (power consumed when the circuit is switching) and static power (power consumed when the circuit is idle).
- **Pin and I/O Information:** The library will specify the input and output pins for each standard cell, including pin names, directions (input or output), and electrical characteristics.
- **Library Files:** These library files often come in various formats, including Liberty (.lib) files, which contain detailed timing and power information, and Verilog models, which allow designers to use these standard cells in their digital designs.
- **Characterization Data:** The library may include data characterizing how the standard cells perform under different operating conditions, including variations in temperature and supply voltage. This helps designers account for variability in their designs.
- **Technology Files:** These files might also include information about the specific characteristics of the SkyWater 130nm process technology, such as transistor models, interconnect information, and other process-related data.
### Hierarchical vs Flat Synthesis
#### Hierarchical Synthesis
- Hierarchical synthesis involves dividing the design into logical modules or blocks and synthesizing each module separately.
- These modules can have their own hierarchies, and they communicate through well-defined interfaces
- It enhances reusability, as individual modules can be reused in other designs.
- Supports better scalability for large, complex designs.
#### Steps to Hierarchical Synthesis
Enter the following commands to run Hierarchial Synthesis
- **1.**```read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  ```
- **2.**```read_verilog multiple_modules.v```
- **3.**```synth -top multiple_modules```
- **5.**```abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib```
- **6.**```show multiple_modules```
- **7.**```write_verilog -noattr multiple_modules_hier.v```
#### Output of Hiererchical Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/f1f6d875-5e63-4930-9bd3-2701bfbfd150)
#### Flat Synthesis
Enter the following commands to run flat Synthesis
- **1.**```read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  ```
- **2.**```read_verilog multiple_modules.v```
- **3.**```synth -top multiple_modules```
- **5.**```abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib```
- **6.**```flatten```
- **7.**```show multiple_modules```
- **8.**```write_verilog -noattr multiple_modules_hier.v```
- **9.**```!gvim multiple_modules_hier.v```
#### Output of Flat Synthesis 
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/6f23e1ed-a7d1-4888-ad05-8e52b994ac35)
## Various Flop Coding Styles and Optimization
### Flop Coding Styles
#### Asynchronous Reset D Flip-Flop
- When an asynchronous reset input is activated (set to '1'), regardless of the clock signal, the stored value is forced to '0'.
- Otherwise, on the positive edge of the clock signal, the stored value is updated with the data input.
#### Asynchronous Set D Flip-Flop
- When an asynchronous set input is activated (set to '1'), regardless of the clock signal, the stored value is forced to '1'.
- Otherwise, on the positive edge of the clock signal, the stored value is updated with the data input.
#### Synchronous Reset D Flip-Flop
- When a synchronous reset input is activated (set to '1') at the positive edge of the clock signal, the stored value is forced to '0'.
- Otherwise, on the positive edge of the clock signal, the stored value is updated with the data input.
#### D Flip-Flop with Asynchronous Reset and Synchronous Reset

- This flip-flop combines both asynchronous and synchronous reset features.
- When the asynchronous reset input is activated (set to '1'), the stored value is immediately forced to '0'.
- When the synchronous reset input is activated (set to '1') at the positive edge of the clock signal, the stored value is forced to '0'.
- Otherwise, on the positive edge of the clock signal, the stored value is updated with the data input.
### Synthesis and Simulation of Flops
#### Asynchronous Reset D Flip-Flop
##### Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/0755fdd9-fe56-411e-9c00-a9f739ccaa44)
##### WaveForm 
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/acb6892a-2530-415d-b92f-8d51b9da93ec)
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/ee48b3c2-0933-48f4-bfd4-a7d9abb5c72e)
#### Asynchronous set D Flip-Flop
##### Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/2be5e071-39f3-4bb1-b8fb-29b3193ee45b)
##### WaveForm
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/2272b536-b9ae-439f-9964-507b5cab9638)
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/c63601d2-cc9e-4d69-a1ad-30b6bbd28946)
#### Asynchronous Reset D Flip-Flop
##### Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/190f5ec6-292a-4f16-8b08-4da3ff7391d4)
##### WaveForm
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/9636aae8-b57a-4030-acba-4797926ec039)
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/409b22a7-c008-46aa-aac2-33f532e1691f)
### Interesting Optimisations
#### Mul_2
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/e1790bd3-8fba-440a-887f-edb026776b75)
##### Schematic
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/fd92356c-6094-4f27-b017-e29d446e74c2)
#### Mul_8
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/b1c3ae7b-891f-49f5-85be-1ff3a19c263d)
##### Schematic
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/8c0cef16-7af6-498d-be90-7d6bc167089e)


##### * All the codes and output netlist are available in the files 
