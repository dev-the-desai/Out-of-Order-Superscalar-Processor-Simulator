# Out-of-Order-Superscalar-Processor-Simulator
A cycle-accurate simulator for an out-of-order superscalar processor that models dynamic instruction scheduling with configurable pipeline width, issue queue size, and reorder buffer capacity.

This simulator models a detailed out-of-order execution pipeline with perfect caches and branch prediction. It focuses on data dependencies through registers, pipeline stages, and structural hazards in the Issue Queue and Reorder Buffer.
Key Features
Microarchitectural Components

Register Files: 67 architectural registers (R0-R66)
Function Units: Configurable number of universal pipelined FUs
Issue Queue: Dynamic size configuration
Reorder Buffer: Dynamic size configuration
Pipeline Width: Configurable superscalar width

Pipeline Stages

Fetch: Reads instructions from trace file
Decode: Initial instruction processing
Rename: Register renaming and ROB allocation
Register Read: Source operand readiness check
Dispatch: Issue queue management
Issue: Out-of-order instruction issuing
Execute: Pipelined execution with varying latencies
Writeback: Result writeback handling
Retire: In-order instruction retirement

Instruction Types

Type 0: Single cycle latency
Type 1: Two cycle latency
Type 2: Five cycle latency

Technical Details
Input Format
Copy<PC> <operation type> <dest reg #> <src1 reg #> <src2 reg #>
Example:
Copyab120024 0 1 2 3
ab120028 1 4 1 3
ab12002c 2 -1 4 7
Command Line Interface
bashCopy./sim <ROB_SIZE> <IQ_SIZE> <WIDTH> <tracefile>
Output Format
Per-instruction timing:
Copy<seq_no> fu{<op_type>} src{<src1>,<src2>} dst{<dst>} 
FE{<begin-cycle>,<duration>} DE{...} RN{...} RR{...} DI{...} IS{...} EX{...} WB{...} RT{...}
Final Statistics:

Dynamic instruction count
Total execution cycles
Instructions per cycle (IPC)

Implementation Details
Pipeline Registers

DE: Fetch to Decode (WIDTH)
RN: Decode to Rename (WIDTH)
RR: Rename to Register Read (WIDTH)
DI: Register Read to Dispatch (WIDTH)
IQ: Dispatch to Issue (IQ_SIZE)
Execute List: Issue to Execute (WIDTH*5)
WB: Execute to Writeback (WIDTH*5)
ROB: Writeback to Retire (ROB_SIZE)

Key Features

Register renaming with RMT
Out-of-order execution
In-order retirement
Wake-up and select logic
Structural hazard handling
Dynamic scheduling

Build Instructions

Clone the repository
Ensure C/C++/Java compiler is installed
Use provided Makefile to compile

bashCopymake
Usage Example
bashCopy./sim 64 16 2 trace.txt
Testing Framework

Validation runs provided
Cycle-accurate timing verification
Performance metrics comparison
Gradescope auto-grading support

Performance Considerations

O3 optimization support
Debugging symbols for development
Efficiency considerations for large traces
Runtime optimization guidelines

Requirements

C/C++/Java compiler
Make build system
Standard libraries
Linux/Unix environment
