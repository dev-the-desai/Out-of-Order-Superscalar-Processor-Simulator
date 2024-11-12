# Out-of-Order-Superscalar-Processor-Simulator
A cycle-accurate simulator for an out-of-order superscalar processor that models dynamic instruction scheduling with configurable pipeline width, issue queue size, and reorder buffer capacity.

## Project Overview

This project implements a detailed simulator for an out-of-order superscalar processor that can fetch and issue N instructions per cycle. The simulator focuses on modeling data dependencies, pipeline stages, and structural hazards through the Issue Queue and Reorder Buffer.

## Key Implementation Features

1. Pipeline Stages
   * Fetch/Decode/Rename
   * Register Read/Dispatch
   * Issue/Execute
   * Writeback/Retire
   * Support for multiple instructions per cycle

2. Dynamic Scheduling Components
   * Reorder Buffer (ROB) for in-order retirement
   * Issue Queue (IQ) for out-of-order execution
   * Register renaming with Rename Map Table
   * Universal pipelined function units

3. Architectural Features
   * Configurable superscalar width
   * Multiple function units with varying latencies
   * Register dependency tracking
   * In-order fetch and retire, out-of-order execution

## Technical Details

### Processor Parameters
* `ROB_SIZE`: Number of Reorder Buffer entries
* `IQ_SIZE`: Number of Issue Queue entries
* `WIDTH`: Superscalar width (instructions per cycle)
* 67 architectural registers (R0-R66)

### Execution Units
* WIDTH universal pipelined function units
* Operation types with different latencies:
  * Type 0: 1 cycle
  * Type 1: 2 cycles
  * Type 2: 5 cycles

### Microarchitectural Overview
<div align="center">
<img width="800" alt="config supported" src="https://github.com/user-attachments/assets/35a37e6e-9079-4ad7-87b6-a3cc366692a7">
</div>

## Simulator Usage
```bash
./sim <ROB_SIZE> <IQ_SIZE> <WIDTH> <tracefile>
```

Example:
```bash
./sim 64 32 4 trace.txt
```

## Input Format

Traces follow the format:
```
<PC> <operation_type> <dest_reg> <src1_reg> <src2_reg>
```
Where:
* `PC`: Program counter (hex)
* `operation_type`: 0, 1, or 2
* Register numbers: -1 to 66 (-1 indicates no register)

## Performance Metrics
* Dynamic instruction count
* Total execution cycles
* Instructions Per Cycle (IPC)
* Per-instruction timing details
* Pipeline stage statistics

## Project Requirements
* C/C++ compiler
* Make build system
* Input trace files

## Build Instructions
```bash
make clean
make
```

## Implementation Notes
* Perfect branch prediction assumed
* Perfect cache operation assumed
* No memory dependencies modeled
* Implements full pipeline with all hazard handling
* Maintains cycle-accurate simulation
* Supports detailed instruction timing analysis

## Output Format
* Per-instruction timing information
* Pipeline stage timestamps
* Overall performance metrics
* Configuration details
* Execution statistics



## Technical Details

### Input Format

```bash
<PC> <operation type> <dest reg #> <src1 reg #> <src2 reg #>
```
Example:

```bash
ab120024 0 1 2 3
ab120028 1 4 1 3
ab12002c 2 -1 4 7
```
### Command Line Interface

```bash
bashCopy./sim <ROB_SIZE> <IQ_SIZE> <WIDTH> <tracefile>
```

### Output Format

Per-instruction timing:

```bash
Copy<seq_no> fu{<op_type>} src{<src1>,<src2>} dst{<dst>} 
FE{<begin-cycle>,<duration>} DE{...} RN{...} RR{...} DI{...} IS{...} EX{...} WB{...} RT{...}
```

Final Statistics:

    - Dynamic instruction count
    - Total execution cycles
    - Instructions per cycle (IPC)

## Implementation Details

### Pipeline Registers

    - DE: Fetch to Decode (WIDTH)
    - RN: Decode to Rename (WIDTH)
    - RR: Rename to Register Read (WIDTH)
    - DI: Register Read to Dispatch (WIDTH)
    - IQ: Dispatch to Issue (IQ_SIZE)
    - Execute List: Issue to Execute (WIDTH*5)
    - WB: Execute to Writeback (WIDTH*5)
    - ROB: Writeback to Retire (ROB_SIZE)

### Key Features

    - Register renaming with RMT
    - Out-of-order execution
    - In-order retirement
    - Wake-up and select logic
    - Structural hazard handling
    - Dynamic scheduling

## Build Instructions

Clone the repository
Ensure C/C++/Java compiler is installed
Use provided Makefile to compile

bashCopymake
Usage Example
bashCopy./sim 64 16 2 trace.txt

## Testing Framework

Validation runs provided
Cycle-accurate timing verification


## Requirements

C/C++/Java compiler
Make build system
Standard libraries


