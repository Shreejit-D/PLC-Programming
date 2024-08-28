# Vacuum Control System Without PID

## Project Overview

This project involves maintaining a vacuum in a system despite rapidly changing environmental conditions without using a PID controller. The system adjusts the vacuum pump speed based on how closely the measured vacuum matches a desired setpoint. The program makes periodic adjustments to the pump speed every 10 seconds, based on the difference between the measured vacuum and the setpoint.

![image](https://github.com/user-attachments/assets/658d30f8-37ea-4d01-8818-e6ed4a679c0c)

## Inputs and Outputs

- **N7:0 - Vacuum Sensor Input**: The measured vacuum value from the sensor, scaled appropriately.
- **N7:1 - Vacuum Pump Output**: The control output to adjust the pump speed.
- **N7:2 - Vacuum Setpoint**: The desired vacuum setpoint (15 in/Hg).
- **N7:3 - Measured Vacuum**: The calculated vacuum level based on the sensor input.

## Operation Logic

1. **Initial Setup**:
   - The system periodically compares the measured vacuum (N7:3) to the setpoint (N7:2).
   - The system adjusts the pump speed (N7:1) every 10 seconds based on the difference between the measured vacuum and the setpoint.

2. **Adjustment Logic**:
   - **Within 4% of Setpoint**: If the measured vacuum is within 4% of the setpoint, no change is made to the pump speed.
   - **Between 4% and 15% Difference**: If the difference is between 4% and 15%, adjust the pump speed by ±20 units.
   - **Between 15% and 30% Difference**: If the difference is between 15% and 30%, adjust the pump speed by ±60 units.
   - **Greater than 30% Difference**: If the difference is greater than 30%, adjust the pump speed by ±100 units.

3. **Important Consideration**:
   - A lower in/Hg value indicates more vacuum, so the logic must account for this inverse relationship when adjusting the pump speed.

## Test Criteria

To verify the system's operation, the following tests should be conducted using Emulate:

1. **Initial Test**:
   - Set N7:0 to 8192 and N7:2 to 15. N7:3 should stabilize around 15.
   - Set N7:1 to 6000 and observe that N7:1 remains unchanged for more than 10 seconds.

2. **4-15% Range Test**:
   - Set N7:0 to 8750. N7:1 should start increasing by 20 units every 10 seconds.
   - Set N7:0 to 7650. N7:1 should start decreasing by 20 units every 10 seconds.

3. **15-30% Range Test**:
   - Set N7:0 to 10000. N7:1 should start increasing by 60 units every 10 seconds.
   - Set N7:0 to 6200. N7:1 should start decreasing by 60 units every 10 seconds.

4. **Greater than 30% Range Test**:
   - Set N7:0 to 13000. N7:1 should start increasing by 100 units every 10 seconds.
   - Set N7:0 to 4000. N7:1 should start decreasing by 100 units every 10 seconds.

## Conclusion

This project provides a custom logic-based approach to maintaining a vacuum in a system without using a PID controller. The system dynamically adjusts the pump speed based on the difference between the measured vacuum and the desired setpoint, ensuring stable operation under varying conditions.
