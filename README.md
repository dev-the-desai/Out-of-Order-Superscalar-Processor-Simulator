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
   * 67 architectural registers (R0-R66)

## Technical Details

### Processor Parameters
* `ROB_SIZE`: Number of Reorder Buffer entries
* `IQ_SIZE`: Number of Issue Queue entries
* `WIDTH`: Superscalar width (instructions per cycle)

### Execution Units
* WIDTH universal pipelined function units
* Operation types with different latencies:
  * Type 0: 1 cycle
  * Type 1: 2 cycles
  * Type 2: 5 cycles

### Microarchitectural Overview

<div align="center">
<img width="600" alt="config supported" src="https://github.com/user-attachments/assets/74e0bacb-2c05-46c8-9c0a-4f1a92604a22">
</div>

## Simulator Usage
```bash
./sim <ROB_SIZE> <IQ_SIZE> <WIDTH> <tracefile>
```

Example:
```bash
./sim 64 32 4 trace.txt
```

## Performance Metrics
* Dynamic instruction count
* Total execution cycles
* Instructions Per Cycle (IPC)
* Per-instruction timing details
* Pipeline stage statistics

## Input Format

Traces follow the format:
```
<PC> <operation_type> <dest_reg> <src1_reg> <src2_reg>
```
Where:
* `PC`: Program counter (hex)
* `operation_type`: 0, 1, or 2
* Register numbers: -1 to 66 (-1 indicates no register)

Example:

```bash
ab120024 0 1 2 3
ab120028 1 4 1 3
ab12002c 2 -1 4 7
```

## Output Format
Per-instruction timing:

```bash
<seq_no> fu{<op_type>} src{<src1>,<src2>} dst{<dst>} 
FE{<begin-cycle>,<duration>} DE{...} RN{...} RR{...} DI{...} IS{...} EX{...} WB{...} RT{...}
```

example:

```bash
5 fu{2} src{15,-1} dst{16} FE{5,1} DE{6,1} RN{7,1} RR{8,1} DI{9,1} IS{10,3} EX{13,5} WB{18,1} RT{19,1}
```

Final Statistics:

* Dynamic instruction count
* Total execution cycles
* Instructions per cycle (IPC)

## Implementation Notes
* Perfect branch prediction assumed
* Perfect cache operation assumed
* No memory dependencies modeled
* Implements full pipeline with all hazard handling
* Maintains cycle-accurate simulation
* Supports detailed instruction timing analysis

## Project Requirements
* C/C++ compiler
* Make build system
* Input trace files

## Build Instructions
```bash
make clean
make
```

## Testing Framework

Prepare trace files in correct format
Run simulator with desired configuration
Analyze output metrics and instruction contents


