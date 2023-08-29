# Day6
### GLS Synthesis-Simulation Mismatch and Blocking Non-blocking Statements
GLS Concepts And Flow Using Iverilog
-   **Gate Level Simualtion**
    -   Gate-level simulation is a technique used in digital design and verification to validate the functionality of a digital circuit at the gate-level implementation.
    -   It involves simulating the circuit using the actual logic gates and flip-flops that make up the design, as opposed to higher-level abstractions like RTL (Register Transfer Level) descriptions.
    -   This type of simulation is typically performed after the logic synthesis process, where a high-level description of the design is transformed into a netlist of gates and flip-flops.
    -   We perform this to verify logical correctness of the design after synthesizing it. Also ensuring the timing of the design is met.
<img width="608" alt="263759047-6298b067-2f45-4dbc-ad25-762ac3d8be63" src="https://github.com/KKiranR/pes_asic_class/assets/89727621/ff65a770-7f34-4167-89d3-c1d01553ac39">

**Synthesis-Simulation Mismatch**
    
   -   A synthesis-simulation mismatch refers to a situation in digital design where the behavior of a circuit, as observed during simulation, doesn't match the expected or desired behavior of the circuit after it has been synthesized.
    -   This discrepancy can occur due to various reasons, such as timing issues, optimization conflicts, and differences in modeling between the simulation and synthesis tools.
    -   This mismatch is a critical concern in digital design because it indicates that the actual hardware implementation might not perform as expected, potentially leading to functional or timing failures in the fabricated chip.
-   **Blocking Statements**
    
    -   Blocking statements are executed sequentially in the order they appear in the code and have an immediate effect on signal assignments.
      Example:
```  verilog
 module BlockingExample(input A, input B, input C, output Y, output Z);
      wire temp;
    
      // Blocking assignment
      assign temp = A & B;
    
      always @(posedge C) begin
          // Blocking assignment
          Y = temp;
          Z = ~temp;
      end
     endmodule
   ```
**Non-Blocking Statements**
    
-   Non-blocking assignments are used to model concurrent signal updates, where all assignments are evaluated simultaneously and then scheduled to be updated at the end of the time step.
      Example:
     ``` verilog
     module NonBlockingExample(input clock, input D, input reset, output reg Q);
    
     always @(posedge clock or posedge reset) begin
         if (reset)
             Q <= 0;  // Reset the flip-flop
         else
             Q <= D;  // Non-blocking assignment to update Q with D on clock edge
     end
    endmodule
    ```
**Caveats with Blocking Statements**
    
-   Blocking statements in hardware description languages like Verilog have their uses, but there are certain caveats and considerations to be aware of when working with them. Here are some important caveats associated with using blocking statements:
    -   **Procedural Execution**: Blocking statements are executed sequentially in the order they appear within a procedural block (such as an always block). This can lead to unexpected behavior if the order of execution matters and is not well understood.
    -   **Lack of Parallelism**: Blocking statements do not accurately represent the parallel nature of hardware. In hardware, multiple signals can update concurrently, but blocking statements model sequential behavior. As a result, using blocking statements for modeling complex concurrent logic can lead to incorrect simulations.
    -  ** Race Conditions**: When multiple blocking assignments operate on the same signal within the same procedural block, a race condition can occur. The outcome of such assignments depends on their order of execution, which might lead to inconsistent or unpredictable behavior.
    -   **Limited Representation of Hardware**: Hardware systems are inherently concurrent and parallel, but blocking statements do not capture this aspect effectively. Using blocking assignments to model complex combinational or sequential logic can lead to models that are difficult to understand, maintain, and debug.
    -   **Combinatorial Loops**: Incorrect use of blocking statements can lead to unintentional combinational logic loops, which can result in simulation or synthesis errors.
    -   **Debugging Challenges**: Debugging code with many blocking assignments can be challenging, especially when trying to track down timing-related issues.
    -   **Not Suitable for Flip-Flops**: Blocking assignments are not suitable for modeling flip-flop behavior. Non-blocking assignments (<=) are generally preferred for modeling flip-flop updates to ensure accurate representation of concurrent behavior.
     -   **Sequential Logic Misrepresentation**: Using blocking assignments to model sequential logic might not capture the intended behavior accurately. Sequential elements like registers and flip-flops are better represented using non-blocking assignments.
    -   **Synthesis Implications**: The behavior of blocking assignments might not translate well during synthesis, leading to potential mismatches between simulation and synthesis results.
##   Lab
### Synthesis-Simulation Mismatch
**GLS to Gate-Level Simulation**
#### Command
``` bash=
      iverilog <give primive .v  file> <give the verilog file for the library .v file > <designfile> <testbench file>
      ./a.out
      gtkwave <.vcd file>
```
####  ternary_operator_mux
##### Normal Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/fcc0c745-31c6-4772-bfa7-5904b4dceb62)
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/0357f36c-2a10-40c8-ac28-60f9e12d9399) ![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/1ec0e919-1516-44dd-81b0-619d7aaee647)
##### GLS to Gate-Level Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/34c25e98-668a-42f8-b4e2-ae992aedc9f0)
####  badmux
##### Normal Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/06c111d6-e855-4e5b-b7fc-716e179ec3c3)
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/869696ec-38b6-4295-9de7-0e2f3b94f4c4) ![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/991d36e3-c365-42b8-abce-80369c088ef3)
##### GLS to Gate-Level Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/3f939db8-2b5d-4503-a8f9-31fc9bfb464f)
### Synth-Sim Mismatch for Blocking Statement
##### blocking_caveat
##### Normal Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/a049135b-9d82-4a0d-9ebe-115bc90697b2)
##### Synthesis
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/73a6126c-6e56-415a-baee-2a9f69b8ffb7) ![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/06d19d52-b7ee-4bf1-99ec-3dde6ac73fd4)
##### GLS to Gate-Level Simulation
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/91f5ec09-c3fd-453f-80b5-edea0ced11a1)
