<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

This design is a **4×4-bit unsigned multiplier** that produces an 8-bit product. The core multiplier (`mult.v`) computes `P = A × B` where A and B are 4-bit inputs.

The Tiny Tapeout top module (`tt_um_mult_top`) connects the 8-bit input bus to the operands: **A** is on `ui_in[7:4]` and **B** is on `ui_in[3:0]`. The 8-bit product **P** is driven on `uo_out[7:0]`. Inputs are sampled on the rising edge of the clock when **ena** (enable) is high; when **rst_n** (reset) is low, A and B are cleared. There is one clock cycle of input delay before the product appears on the outputs (inputs are registered, then the multiplier is combinatorial).

## How to test

1. Drive the 8 input pins: set **A[3:0]** on `ui[4]`–`ui[7]` and **B[3:0]** on `ui[0]`–`ui[3]`.
2. Assert the enable signal so the design samples A and B.
3. After the input register delay, read the 8-bit product **P[7:0]** on `uo[0]`–`uo[7]`.

Example: A = 15 (0xF), B = 15 (0xF) → P = 225 (0xE1). Use reset to clear the operands when needed.

## External hardware

None. The multiplier uses only the standard Tiny Tapeout input/output pins; no PMODs, displays, or other external hardware are required.
