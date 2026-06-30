# Verilog Edge Detector

A simple and efficient digital logic edge detector implemented in Verilog. This module is designed to detect rising edges, falling edges, and transitions (both edges) of an input signal relative to the system clock. It is highly useful for debouncing buttons, synchronizing signals, and triggering state machine transitions in FPGA or ASIC designs.

## Features
- **Rising Edge Detection (Positive Edge):** Outputs a one-clock-cycle high pulse when the input transitions from `0` to `1`.
- **Falling Edge Detection (Negative Edge):** Outputs a one-clock-cycle high pulse when the input transitions from `1` to `0`.
- **Any Edge Detection (Dual Edge):** Outputs a pulse on any logic level transition.
- **Synchronous Design:** Prevents metastability by evaluating the signal predictably on the active clock edge.

## How It Works
The design operates using a standard 2-stage shift register (using D flip-flops) to store the current state and the previous state of the input signal at each clock edge. 
- A **rising edge** is detected when `previous_state == 0` and `current_state == 1`.
- A **falling edge** is detected when `previous_state == 1` and `current_state == 0`.

## Module Interface

```verilog
module edge_detector (
    input wire clk,           // System clock
    input wire rst_n,         // Active-low reset
    input wire signal_in,     // Input signal to monitor
    output wire pe_out,       // Positive (Rising) edge output
    output wire ne_out,       // Negative (Falling) edge output
    output wire any_edge_out  // Any edge output
);
