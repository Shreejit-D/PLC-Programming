# Raw Material Inventory Management System

## Project Overview

This project involves managing the inventory of three raw materials—widgets, doodads, and wockies—using a PLC-based system. Each material is identified by a unique part number, and the system tracks the quantity of each material on hand. The inventory is updated through barcode scans, which provide information about the part number, quantity, and whether the material is incoming or outgoing.

## Inputs and Outputs

- **ST9:0 - Barcode Scan**: Receives input from the barcode scanner in the format `PPP‐QQ:D`, where:
  - `PPP` represents the part number (123 for widgets, 456 for doodads, 789 for wockies).
  - `QQ` represents the quantity.
  - `D` represents the direction (1 for incoming, 2 for outgoing).
- **N7:0 - Widgets On-Hand (Part #123)**: Stores the current quantity of widgets.
- **N7:1 - Doodads On-Hand (Part #456)**: Stores the current quantity of doodads.
- **N7:2 - Wockies On-Hand (Part #789)**: Stores the current quantity of wockies.

## Operation Logic

1. **Initial State**:
   - When the program starts, the quantities in N7:0, N7:1, and N7:2 should all be set to 0.

2. **Incoming Inventory**:
   - When a barcode scan in the format `PPP‐QQ:1` is received, the quantity `QQ` should be added to the respective part number's on-hand quantity.
   - After processing, the value in ST9:0 should automatically reset to a blank or null value.

3. **Outgoing Inventory**:
   - When a barcode scan in the format `PPP‐QQ:2` is received, the quantity `QQ` should be subtracted from the respective part number's on-hand quantity.
   - As with incoming scans, the value in ST9:0 should reset immediately after processing.

4. **Unrecognized Part Numbers**:
   - If a barcode scan contains an unrecognized part number, the system should ignore the input without affecting the inventory or causing errors.

## Test Criteria

To verify the functionality of the system, the following tests should be performed using Emulate:

1. **Initial Test**:
   - Run the program and check that N7:0, N7:1, and N7:2 are all equal to 0.

2. **First Incoming Scan**:
   - Set the value of ST9:0 to `123‐10:1`. After processing, N7:0 should be 10, and N7:1 and N7:2 should remain 0. The value of ST9:0 should reset automatically.

3. **Second Incoming Scan**:
   - Without changing the value of ST9:0 between steps, set it to `123‐10:1` again. N7:0 should now be 20, with N7:1 and N7:2 still at 0.

4. **Different Part Incoming Scans**:
   - Set ST9:0 to `456‐15:1`. After processing, N7:0 should be 20, N7:1 should be 15, and N7:2 should remain 0.
   - Set ST9:
