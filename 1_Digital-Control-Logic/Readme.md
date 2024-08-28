# Compressor Pressure Control System

## Project Overview

This project is focused on maintaining the pressure in a receiver of a compressor application using a programmable logic controller (PLC). The system utilizes two pressure switches to manage the operation of a pump and an indicator light, ensuring that the pressure remains within a desired range.

![image](https://github.com/user-attachments/assets/8fcbfedd-34d1-4304-a637-1a6e173b4368)

## Inputs and Outputs

- **I:0/0 - Low Pressure Switch**: Closes when the pressure reaches 90 psi or above.
- **I:0/1 - High Pressure Switch**: Closes when the pressure reaches 110 psi or above.
- **O:0/0 - Pressure Pump**: Operates to maintain the system's pressure.
- **O:0/1 - Pressure Indicator Light**: Illuminates when the pressure exceeds 90 psi.

## Operation Logic

1. **Initial State**:
   - Upon starting the program, the pump (O:0/0) should start immediately.
   - The pressure indicator light (O:0/1) should remain off.

2. **Low Pressure Activation**:
   - When the low pressure switch (I:0/0) closes at 90 psi, the pump should stay energized.
   - The pressure indicator light should turn on.

3. **High Pressure Activation**:
   - If the high pressure switch (I:0/1) closes at 110 psi, the pump should deenergize.
   - The pressure indicator light should remain on.

4. **High Pressure Deactivation**:
   - If the high pressure switch is deactivated (open) while the low pressure switch remains closed, the pump should remain deenergized.
   - The pressure indicator light should stay on.

5. **Low Pressure Deactivation**:
   - When both pressure switches are off, the pump should restart, and the pressure indicator light should turn off.

## Test Criteria

The following steps are used to test the program using the Emulate software:

1. **Initial Test**: Verify that the pump starts immediately and the light is off.
2. **Low Pressure Switch On**: Force the low pressure switch on (closed). The pump should remain on, and the light should turn on.
3. **High Pressure Switch On**: With the low pressure switch still on, force the high pressure switch on as well. The pump should turn off, but the light should stay on.
4. **High Pressure Switch Off**: Leave the low pressure switch on and turn off the high pressure switch. The pump should stay off, and the light should remain on.
5. **Both Switches Off**: Finally, force both switches off. The pump should restart, and the light should go off.

## Conclusion

This project demonstrates a simple control system to maintain pressure within a compressor application, ensuring both safety and efficiency by controlling a pump and providing visual feedback through an indicator light.
