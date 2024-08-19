# Conveyor Belt Box Filling System

## Project Overview

This project involves controlling a conveyor belt system that processes boxes with colored labels. The system uses various sensors to determine the position of the box and its label color, which dictates whether the box should be filled with pecans or walnuts. The system also monitors the fill level of each box and moves the box forward once it's full.

![image](https://github.com/user-attachments/assets/859d5599-2dba-416c-ae02-37c1c974a05d)

## Inputs and Outputs

- **I:0/0 - Proximity Switch**: Closes when a box is near the filling station.
- **I:0/1 - Level Switch**: Closes when the box is full.
- **I:0/2 - Red Photo Eye**: Closes when a red label is detected on the box.
- **I:0/3 - Blue Photo Eye**: Closes when a blue label is detected on the box.
- **O:0/0 - Conveyor Motor**: Operates to move the conveyor forward when activated.
- **O:0/1 - Walnut Hopper**: Activates to fill the box with walnuts when the blue label is detected.
- **O:0/2 - Pecan Hopper**: Activates to fill the box with pecans when the red label is detected.

## Operation Logic

1. **Initial State**:
   - When the program starts, the conveyor motor (O:0/0) should start running immediately.
   - Both the walnut hopper (O:0/1) and pecan hopper (O:0/2) should remain off.

2. **Box Detection**:
   - When the proximity switch (I:0/0) closes as a box arrives, the conveyor motor should stop.
   - Both hoppers should remain deenergized until a label is detected.

3. **Red Label Detection**:
   - If the red photo eye (I:0/2) closes, indicating a red label, the pecan hopper (O:0/2) should energize to fill the box with pecans.
   - The conveyor motor and walnut hopper should remain off.

4. **Blue Label Detection**:
   - If the red photo eye is off and the blue photo eye (I:0/3) closes, indicating a blue label, the walnut hopper (O:0/1) should energize to fill the box with walnuts.
   - The conveyor motor should remain off, and the pecan hopper should be deenergized.

5. **Box Filling Completion**:
   - When the level switch (I:0/1) closes, indicating the box is full, both hoppers should deenergize.
   - The conveyor motor should restart to move the filled box forward.

6. **Final State**:
   - Once the box has moved on, with the proximity switch, level switch, and both photo eyes off, the conveyor should continue running, and both hoppers should remain off.

7. **Bonus Test**:
   - If both photo eyes are forced on while the proximity and level switches are open, neither hopper should energize, ensuring no product is released without a box to catch it.

## Test Criteria

To ensure the system operates correctly, the following tests should be conducted using Emulate:

1. **Initial Test**: Verify that the conveyor motor starts immediately, with both hoppers off.
2. **Box Detection**: Force the proximity switch on. The conveyor motor should stop, and both hoppers should remain off.
3. **Red Label Filling**: With the proximity switch closed, force the red photo eye on. The pecan hopper should energize, while the walnut hopper and conveyor motor should remain off.
4. **Blue Label Filling**: With the proximity switch closed, force the red photo eye off and the blue photo eye on. The walnut hopper should energize, while the pecan hopper should turn off and the conveyor motor should remain off.
5. **Box Full**: Force the level switch on. Both hoppers should deenergize, and the conveyor motor should restart to move the box forward.
6. **Final State**: Force all switches and photo eyes off. The conveyor motor should keep running, and both hoppers should remain deenergized.
7. **Bonus Test**: With the proximity and level switches open, force both photo eyes on. Ensure neither hopper energizes.

## Conclusion

This project implements an automated system to accurately fill boxes with different products based on label color and ensures that the boxes are filled to the correct level before moving them forward on the conveyor belt. The system is designed with safety checks to prevent product waste.
