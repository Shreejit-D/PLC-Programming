# Plant Runtime Tracking System

## Project Overview

This project involves creating a system to track the runtime of a host plant. The system monitors when the plant is running and accumulates the total runtime in seconds, minutes, hundreds of hours, and thousands of hours. Additionally, the system includes a reset button that allows the user to clear the accumulated runtime and start fresh.

## Inputs and Outputs

- **I:0/0 - System Running**: Receives a signal indicating that the plant is running.
- **N7:0 - Seconds**: Accumulates the runtime in seconds.
- **N7:1 - Minutes**: Accumulates the runtime in minutes.
- **N7:2 - Hundreds of Hours**: Accumulates the runtime in hundreds of hours.
- **N7:3 - Thousands of Hours**: Accumulates the runtime in thousands of hours.
- **B3:0/0 - Reset Button**: Resets all accumulated runtime values to zero.

## Operation Logic

1. **Initial State**:
   - Upon starting the program, the accumulators (N7:0 - N7:3) should all be set to zero.
   - No values should change until the system receives a running signal.

2. **Runtime Accumulation**:
   - When the system running input (I:0/0) is activated (closed), N7:0 should begin counting seconds, cycling from 0 to 59 repeatedly.
   - Each time N7:0 reaches 60 seconds, it resets to 0, and N7:1 increments by one minute.
   - N7:1 should count up to 59 minutes before resetting to 0, at which point N7:2 increments by one (hundreds of hours).
   - N7:2 should continue counting until it reaches 999, after which it resets to 0, and N7:3 increments by one (thousands of hours).

3. **Pause and Resume Counting**:
   - When the system running input (I:0/0) is deactivated (open), all accumulators should pause and maintain their current values.
   - If the system running input is activated again, the accumulators should resume counting from where they left off.

4. **Reset Functionality**:
   - Activating the reset button (B3:0/0) should immediately reset all accumulators (N7:0 - N7:3) to zero, allowing for a fresh start in tracking runtime.

## Test Criteria

To ensure the system operates correctly, the following tests should be conducted using Emulate:

1. **Initial Test**:
   - Run the program and verify that N7:0 - N7:3 are all set to zero and remain unchanged.

2. **Runtime Accumulation Test**:
   - Force the system running input (I:0/0) on. Observe that N7:0 starts accumulating seconds, cycling from 0 to 59.
   - Verify that N7:1 increments by one each time N7:0 reaches 60 seconds.
   - Manually adjust N7:1 and N7:2 to their limits to verify that N7:2 and N7:3 accumulate correctly when their respective lower units roll over.

3. **Pause and Resume Test**:
   - Force the system running input (I:0/0) off and confirm that all accumulators freeze.
   - Reactivate the system running input and confirm that the accumulators resume from where they left off.

4. **Reset Test**:
   - Activate the reset button (B3:0/0) and verify that all accumulators (N7:0 - N7:3) reset to zero.

## Conclusion

This project successfully tracks the runtime of a plant by accumulating the time in seconds, minutes, hundreds of hours, and thousands of hours. The system is designed to pause and resume counting based on the plant's operational status, with a convenient reset function to clear the accumulated time for a fresh start.
