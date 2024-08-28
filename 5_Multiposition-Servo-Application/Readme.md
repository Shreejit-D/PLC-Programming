# Modular Water Treatment System Integration

## Project Overview

This project involves the integration of a modular water treatment system into an existing system. The system controls a servo-operated valve that cycles through various positions (Home, Fill, Drain, Flush) based on a cycle call from the host system. The valve positions are monitored using cam-operated microswitches, and the system can be enhanced with additional features to track the valve's position and handle interrupts.

![image](https://github.com/user-attachments/assets/ffcb1396-de74-425f-ab49-d01733060c2f)

## Inputs and Outputs

### Primary IO:
- **I:0/0 - Home Microswitch**: Closes when the valve is in the home position.
- **I:0/1 - Fill Microswitch**: Closes when the valve is in the fill position.
- **I:0/2 - Drain Microswitch**: Closes when the valve is in the drain position.
- **I:0/3 - Flush Microswitch**: Closes when the valve is in the flush position.
- **I:0/4 - Cycle Call**: Signal closes when the host system requires a cycle.
- **O:0/0 - Servo**: Energizes to move the valve to the next position.

### Bonus IO:
- **N7:0 - Valve Position Integer**: Tracks the current valve position with values:
  - `0 = HOME`
  - `1 = FILL`
  - `2 = DRAIN`
  - `3 = FLUSH`
  - `4 = TRAVELLING` (between positions)
- **B3:0/0 - Reset / Cycle Interrupt Button**: Aborts the current process and returns the valve to the home position.

## Operation Logic

1. **Initial State**:
   - Upon starting the program, the servo (O:0/0) should energize immediately, moving the valve to the home position.
   - If the bonus feature is implemented, N7:0 should initially be set to `4` (TRAVELLING).

2. **Position Detection**:
   - **Fill Position**: If the fill microswitch (I:0/1) is closed, the servo remains energized, and N7:0 should be `1`.
   - **Home Position**: If the home microswitch (I:0/0) is closed, the servo should deenergize, and N7:0 should be `0`.

3. **Cycle Call**:
   - When the cycle call (I:0/4) is momentarily activated, the servo should energize, preparing for the next cycle. N7:0 should remain `0` until the valve leaves the home position.

4. **Filling Cycle**:
   - When the fill microswitch (I:0/1) is closed after leaving home, N7:0 should be set to `1`, and the servo should deenergize for 10 seconds before automatically re-energizing to move to the next position.

5. **Draining Cycle**:
   - After filling, if the drain microswitch (I:0/2) is closed, N7:0 should be set to `2`, and the servo should deenergize for 20 seconds before automatically re-energizing.

6. **Flushing Cycle**:
   - After draining, if the flush microswitch (I:0/3) is closed, N7:0 should be set to `3`, and the servo should deenergize for 10 seconds before automatically re-energizing.

7. **Returning to Home**:
   - After flushing, the valve returns to the home position when the home microswitch (I:0/0) is closed. N7:0 should be set to `0`, and the servo should deenergize and remain off.

## Bonus Features

1. **Valve Position Tracking**:
   - The system uses N7:0 to report the current valve position, with states for Home, Fill, Drain, Flush, and Travelling.

2. **Reset / Interrupt Functionality**:
   - A reset button (B3:0/0) can be used to interrupt the process and immediately return the valve to the home position, setting N7:0 to `0` and deenergizing the servo.

## Test Criteria

To ensure the system operates correctly, the following tests should be conducted using Emulate:

1. **Initial Test**:
   - Run the program and verify that the servo energizes immediately. If the bonus feature is implemented, N7:0 should be `4` (TRAVELLING).

2. **Fill Position Test**:
   - Force the fill microswitch (I:0/1) on. The servo should remain energized, and N7:0 should be `1`.

3. **Home Position Test**:
   - Force the home microswitch (I:0/0) on. The servo should deenergize, and N7:0 should be `0`.

4. **Cycle Call Test**:
   - Momentarily force I:0/4 (Cycle Call) on and then off. The servo should energize again, but N7:0 should remain `0`.

5. **Filling Test**:
   - Force the home microswitch off, and then the fill microswitch on. N7:0 should be `1`, and the servo should deenergize for 10 seconds before re-energizing.

6. **Draining Test**:
   - Force the fill microswitch off, then the drain microswitch on. N7:0 should be `2`, and the servo should deenergize for 20 seconds before re-energizing.

7. **Flushing Test**:
   - Force the drain microswitch off, then the flush microswitch on. N7:0 should be `3`, and the servo should deenergize for 10 seconds before re-energizing.

8. **Return to Home Test**:
   - Force the flush microswitch off, then the home microswitch on. N7:0 should be `0`, and the servo should deenergize and stay off.

## Conclusion

This project successfully integrates a modular water treatment system into an existing system, with a servo-controlled valve that cycles through the necessary positions based on signals from the host system. The project also includes advanced features for tracking valve position and handling interrupts, ensuring a robust and flexible control system.
