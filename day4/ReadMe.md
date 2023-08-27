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
**1.**```read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  ```
**2.**```read_verilog multiple_modules.v```
**3.**```synth -top multiple_modules```
**5.**```abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib```
**6.**```show multiple_modules```
**7.**```write_verilog -noattr multiple_modules_hier.v```
#### Output of Hiererchical Synthesis
![](https://hackmd.io/_uploads/HJZa_5_6h.png)
#### Flat Synthesis
Enter the following commands to run flat Synthesis
**1.**```read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  ```
**2.**```read_verilog multiple_modules.v```
**3.**```synth -top multiple_modules```
**5.**```abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib```
**6.**```flatten```
**7.**```show multiple_modules```
**8.**```write_verilog -noattr multiple_modules_hier.v```
**9.**```!gvim multiple_modules_hier.v```
#### Output of Flat Synthesis 
![](https://hackmd.io/_uploads/ByfHFqOph.png)
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
![](https://hackmd.io/_uploads/HJQXaquT2.png)
##### WaveForm 
![](https://hackmd.io/_uploads/SJ0469_ph.png)
##### Synthesis
![](https://hackmd.io/_uploads/SyEpT5_ah.png)
#### Asynchronous set D Flip-Flop
##### Simulation
![](https://hackmd.io/_uploads/r1U9A5Opn.png)
##### WaveForm
![](https://hackmd.io/_uploads/BkOKR5ua3.png)
##### Synthesis
![](https://hackmd.io/_uploads/B1MyyiOah.png)
#### Asynchronous Reset D Flip-Flop
##### Simulation
![](https://hackmd.io/_uploads/ryOckiOTh.png)
##### WaveForm
![](https://hackmd.io/_uploads/Hkoxeju63.png)
##### Synthesis
![](https://hackmd.io/_uploads/BJcyxiOpn.png)
### Interesting Optimisations
#### Mul_2
##### Synthesis
![](https://hackmd.io/_uploads/H1frWsOp3.png)
##### Schematic
![](https://hackmd.io/_uploads/H138bj_ph.png)
#### Mul_8
##### Synthesis
![](https://hackmd.io/_uploads/rkPUGsOTh.png)
##### Schematic
![](https://hackmd.io/_uploads/BkXDfju63.png)


##### * All the codes and output netlist are available in the files 