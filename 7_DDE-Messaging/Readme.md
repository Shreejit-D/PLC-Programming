# Machine Cycle Tracking System

## Project Overview

This project involves setting up a machine that continuously cycles between two modes, each executing two functions. The system tracks the current mode and function names, counts the number of cycles completed for each mode-function combination, and stores these details. The data, including mode names, function names, and cycle counts, can be exported to an Excel workbook on demand.

![image](https://github.com/user-attachments/assets/39cb93ba-dfd7-4f23-a99d-3c2795870a90)

## Inputs and Outputs

- **ST9:0 - Mode**: Stores the current mode as a string (e.g., "Mode-1", "Mode-2").
- **ST9:1 - Function**: Stores the current function as a string (e.g., "F1", "F2").
- **ST9:2 - Mode + Function**: Stores the combined mode and function as a string (e.g., "Mode-1 F1").
- **N7:0 - M1F1 Cycles**: Counts the number of cycles completed for Mode-1 and Function-1.
- **N7:1 - M1F2 Cycles**: Counts the number of cycles completed for Mode-1 and Function-2.
- **N7:2 - M2F1 Cycles**: Counts the number of cycles completed for Mode-2 and Function-1.
- **N7:3 - M2F2 Cycles**: Counts the number of cycles completed for Mode-2 and Function-2.

## Operation Logic

1. **Mode and Function Cycling**:
   - The machine continuously cycles between two modes (Mode-1 and Mode-2).
   - Each mode has two functions (F1 and F2), with each function running for 10 seconds.
   - The system updates the current mode, function, and combined mode-function strings every 10 seconds.

2. **Cycle Counting**:
   - The system increments the appropriate cycle counter (N7:0 - N7:3) each time a new mode-function cycle begins.
   - The cycle counts follow this pattern: (0,0,0,0), (1,0,0,0), (1,1,0,0), (1,1,1,0), (1,1,1,1), (2,1,1,1), and so on.

3. **Data Export to Excel**:
   - On demand, the system exports the current mode, function, combined mode-function strings, and cycle counts to an Excel workbook.

## Test Criteria

To ensure the system operates correctly, the following tests should be conducted using Emulate:

1. **Initial Mode and Function Cycling**:
   - Run the program and observe that the modes and functions begin cycling every 10 seconds.
   - Verify that the strings in ST9:0 (Mode), ST9:1 (Function), and ST9:2 (Mode + Function) update accordingly with each cycle.

2. **Cycle Counting**:
   - Verify that the cycle counters (N7:0 - N7:3) increment correctly as the system progresses through each mode-function combination.
   - The counters should follow the expected sequence as new cycles are initiated.

3. **Excel Data Export**:
   - Open the Excel workbook and press the designated button to trigger data export.
   - Confirm that the sheet updates with the current values of all strings (ST9:0 - ST9:2) and integers (N7:0 - N7:3).

## Conclusion

This project successfully implements a machine cycle tracking system that monitors and records the current mode, function, and cycle counts. The data can be exported to an Excel workbook, providing a convenient way to analyze the system's performance. This setup is ideal for applications where continuous monitoring and data logging are required.
