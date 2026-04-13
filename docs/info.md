<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

This project implements a **3-bit adder/subtractor** using fundamental digital logic gates (XOR, AND, OR, and NOT). The circuit performs arithmetic operations between two 3-bit binary numbers A and B, controlled by a mode signal M.

The operation is based on the two’s complement principle:

* When **M = 0**, the circuit performs addition:
  A + B

* When **M = 1**, the circuit performs subtraction:
  A − B = A + (NOT B) + 1

To achieve this behavior, each bit of operand B is conditionally inverted using XOR gates controlled by M:

B' = B ⊕ M

This allows the same hardware to switch between addition and subtraction.

The system is structured as a **ripple-carry architecture**, where each bit stage includes:

* A XOR stage for sum calculation
* AND and OR gates for carry generation
* Carry propagation from one stage to the next

Each stage computes:

* Sum bit:
  S = A ⊕ B' ⊕ Carry_in

* Carry out:
  Cout = (A · B') + (Carry_in · (A ⊕ B'))

The initial carry input is defined as:

* Carry_in = M

This ensures correct two’s complement subtraction when M = 1.

The outputs of the system include:

* Three sum bits (S0, S1, S2)
* One final carry/borrow output (Cout)

Additional outputs may be exposed for debugging or visualization purposes using LEDs.

---

## How to test

To test the system, follow these steps:

1. **Set input values:**

   * Assign binary values to inputs A[2:0] and B[2:0] using switches.
   * Select operation mode:

     * M = 0 → Addition
     * M = 1 → Subtraction

2. **Observe outputs:**

   * The outputs S0, S1, and S2 represent the result.
   * Cout indicates carry (in addition) or borrow behavior (in subtraction).

3. **Recommended test cases:**

   * Addition:

     * A = 011 (3), B = 001 (1), M = 0 → Result = 100 (4)
     * A = 111 (7), B = 001 (1), M = 0 → Result = 1000 (overflow)

   * Subtraction:

     * A = 011 (3), B = 001 (1), M = 1 → Result = 010 (2)
     * A = 001 (1), B = 011 (3), M = 1 → Result = negative (two’s complement)

4. **Validation criteria:**

   * Check that the sum matches expected binary arithmetic.
   * Verify carry propagation across all bits.
   * Confirm correct inversion of B when M = 1.

---

## External hardware

This project is designed for simulation in Wokwi and Tiny Tapeout environments, but conceptually it uses standard digital hardware components:

* Digital input switches (for A, B, and mode M)
* Push buttons (optional for reset or clock control)
* LEDs (for output visualization)
* Logic gates (XOR, AND, OR, NOT)

No external hardware modules (such as PMODs or displays) are required. The design is fully combinational and can be implemented directly in ASIC or FPGA environments.
