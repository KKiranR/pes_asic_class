# Day6
### GLS Synthesis-Simulation Mismatch and Blocking Non-blocking Statements
GLS Concepts And Flow Using Iverilog
-   **Gate Level Simualtion**
    -   Gate-level simulation is a technique used in digital design and verification to validate the functionality of a digital circuit at the gate-level implementation.
    -   It involves simulating the circuit using the actual logic gates and flip-flops that make up the design, as opposed to higher-level abstractions like RTL (Register Transfer Level) descriptions.
    -   This type of simulation is typically performed after the logic synthesis process, where a high-level description of the design is transformed into a netlist of gates and flip-flops.
    -   We perform this to verify logical correctness of the design after synthesizing it. Also ensuring the timing of the design is met.
 Need to add a photo
 ![image]
 -   **Synthesis-Simulation Mismatch**
    
    -   A synthesis-simulation mismatch refers to a situation in digital design where the behavior of a circuit, as observed during simulation, doesn't match the expected or desired behavior of the circuit after it has been synthesized.
    -   This discrepancy can occur due to various reasons, such as timing issues, optimization conflicts, and differences in modeling between the simulation and synthesis tools.
    -   This mismatch is a critical concern in digital design because it indicates that the actual hardware implementation might not perform as expected, potentially leading to functional or timing failures in the fabricated chip.
   -   **Blocking Statements**
    
    -   Blocking statements are executed sequentially in the order they appear in the code and have an immediate effect on signal assignments.
      Example:
```    verilog
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
-   **Non-Blocking Statements**
    
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
   -   **Caveats with Blocking Statements**
    
    -   Blocking statements in hardware description languages like Verilog have their uses, but there are certain caveats and considerations to be aware of when working with them. Here are some important caveats associated with using blocking statements:
        -   Procedural Execution: Blocking statements are executed sequentially in the order they appear within a procedural block (such as an always block). This can lead to unexpected behavior if the order of execution matters and is not well understood.
        -   Lack of Parallelism: Blocking statements do not accurately represent the parallel nature of hardware. In hardware, multiple signals can update concurrently, but blocking statements model sequential behavior. As a result, using blocking statements for modeling complex concurrent logic can lead to incorrect simulations.
        -   Race Conditions: When multiple blocking assignments operate on the same signal within the same procedural block, a race condition can occur. The outcome of such assignments depends on their order of execution, which might lead to inconsistent or unpredictable behavior.
        -   Limited Representation of Hardware: Hardware systems are inherently concurrent and parallel, but blocking statements do not capture this aspect effectively. Using blocking assignments to model complex combinational or sequential logic can lead to models that are difficult to understand, maintain, and debug.
        -   Combinatorial Loops: Incorrect use of blocking statements can lead to unintentional combinational logic loops, which can result in simulation or synthesis errors.
        -   Debugging Challenges: Debugging code with many blocking assignments can be challenging, especially when trying to track down timing-related issues.
        -   Not Suitable for Flip-Flops: Blocking assignments are not suitable for modeling flip-flop behavior. Non-blocking assignments (<=) are generally preferred for modeling flip-flop updates to ensure accurate representation of concurrent behavior.
        -   Sequential Logic Misrepresentation: Using blocking assignments to model sequential logic might not capture the intended behavior accurately. Sequential elements like registers and flip-flops are better represented using non-blocking assignments.
        -   Synthesis Implications: The behavior of blocking assignments might not translate well during synthesis, leading to potential mismatches between simulation and synthesis results.
      ## Lab
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
##### Synthesis
##### GLS to Gate-Level Simulation
####  badmux
##### Normal Simulation
##### Synthesis
##### GLS to Gate-Level Simulation
### Synth-Sim Mismatch for Blocking Statement
##### blocking_caveat
##### Normal Simulation
##### Synthesis
##### GLS to Gate-Level Simulation
