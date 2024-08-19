# Oil Flow Measurement Using Digital Rotameter

## Project Overview

This project involves using a digital rotameter to measure the flow of oil through a pipeline. The rotameter sends a pulse for every 6.3 gallons of oil that flow past it, known as the rotameter’s "k-factor." The system simulates these pulses using a timer, and the flow rate is calculated and updated every 12 seconds. The flow rate is stored in a specified floating-point memory address.

![image](https://github.com/user-attachments/assets/997648a3-2ec4-43ce-882c-40235ad571a2)

## Inputs and Outputs

- **B3:0/0 - Rotameter Pulse Bit**: Simulates the pulse signal from the rotameter, indicating 6.3 gallons of oil flow for each pulse.
- **F8:0 - Flow Rate (gpm)**: Stores the calculated flow rate in gallons per minute (gpm).

## Operation Logic

1. **Initial Pulse Generation**:
   - The system uses a timer to pulse the rotameter bit (B3:0/0) every 12 seconds.
   - Each pulse represents 6.3 gallons of oil flowing through the pipeline.

2. **Flow Rate Calculation**:
   - The flow rate is calculated based on the number of pulses received over the 12-second interval.
   - The formula for the flow rate is: 
     \[
     \text{Flow Rate (gpm)} = \frac{6.3 \text{ gallons/pulse}}{12 \text{ seconds/pulse}} \times 60 \text{ seconds/minute}
     \]
   - This calculation is stored in the F8:0 memory address and updated every 12 seconds.

## Test Criteria

To verify the system's operation, the following tests should be conducted using Emulate:

1. **Initial Test**:
   - Run the program and observe the F8:0 memory address. It should initially be equal to 0.
   - After running for about a minute, the flow rate should stabilize at approximately 31.5 gpm.

2. **Increased Pulse Frequency**:
   - Modify the pulse timer preset from 12 seconds to 2 seconds.
   - After about a minute, the flow rate stored in F8:0 should stabilize at approximately 189 gpm.

## Conclusion

This project successfully simulates the operation of a digit
