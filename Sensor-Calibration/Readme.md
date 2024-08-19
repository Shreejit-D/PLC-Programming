# Oxygen Concentration Measurement and Calibration System

## Project Overview

This project involves developing a system to measure and calibrate the concentration of oxygen (O₂) in the air within a coal mine. The system uses an O₂ sensor that degrades over time, requiring periodic calibration to maintain accuracy. The calibration is done by comparing sensor readings with known concentrations of calibration gases (0% and 30% O₂). The system operates in two cycles: sampling and calibration.

![image](https://github.com/user-attachments/assets/fcbb789c-cff1-4d9f-b620-223af3911360)

### Key Features:
- **Sampling Cycle**: Measures the O₂ concentration in the air continuously.
- **Calibration Cycle**: Compares sensor readings with calibration gases to adjust the sensor's scaling parameters.

## Inputs and Outputs

- **N7:0 - O₂ Sensor Input Signal**: Raw input signal from the O₂ sensor.
- **B3:0/0 - Calibrate Button**: Initiates the calibration cycle.
- **O:0/0 - 0% Gas Valve**: Opens the valve for the 0% O₂ calibration gas.
- **O:0/1 - 30% Gas Valve**: Opens the valve for the 30% O₂ calibration gas.
- **N7:1 - Measured O₂ Concentration**: Displays the measured O₂ concentration in percent (%).
- **N7:2 - O₂ Input Min**: Calibration parameter representing the minimum input signal (default value = 0).
- **N7:3 - O₂ Input Max**: Calibration parameter representing the maximum input signal (default value = 16383).

## Calibration Calculations

During the calibration cycle, the following calculations are used to adjust the sensor's scaling parameters:

- **O₂ Maximum Concentration**: 40%
- **O₂ Calibration Gas Concentration**: 30%
- **O₂ Test Gas Average**: Average reading during the 30% gas period.
- **O₂ Zero Average**: Average reading during the 0% gas period.

### Calibration Formulas:
- **Input Min**: 
  \[
  \text{Input Min} = \text{O₂ Zero Average}
  \]
- **Input Max**: 
  \[
  \text{Input Max} = \left( \frac{\text{O₂ Maximum Concentration}}{\text{O₂ Calibration Gas Concentration}} \times (\text{O₂ Test Gas Average} - \text{O₂ Zero Average}) \right) + \text{O₂ Zero Average}
  \]

## Test Criteria

To verify the system's operation, the following tests should be conducted using Emulate:

1. **Initial Test**:
   - Set N7:0 to 8192, N7:2 to 0, and N7:3 to 16383. N7:1 should display approximately 20%.

2. **Calibration Cycle Test (First Stage)**:
   - Set N7:0 to 0 and toggle B3:0/0 on, then off immediately. During the calibration cycle, set N7:0 to 12288 exactly when the cycle enters the second stage (30% gas). After calibration, N7:1 should be approximately 30%.
   - Set N7:0 to 0; N7:1 should read about 0%. Set N7:0 to 16383; N7:1 should read about 40%.

3. **Calibration Cycle Test (Second Stage)**:
   - Set N7:0 to 100 and toggle B3:0/0 off, then on again immediately. During the calibration cycle, set N7:0 to 11000 exactly when the cycle enters the second stage (30% gas). After calibration, N7:1 should be approximately 30%.
   - Set N7:0 to 100; N7:1 should read about 0%. Set N7:0 to 14633; N7:1 should read about 40%.

## Conclusion

This project implements a robust system to accurately measure and calibrate oxygen concentration in a coal mine environment. The calibration cycle ensures that the sensor remains accurate over time by adjusting its scaling parameters based on readings from known calibration gases. The system's test procedures ensure that the calibration is functioning correctly and the measured values are within expected ranges.
****
