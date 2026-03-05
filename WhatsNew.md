# RadASM 2.2.3.0

## Key Compatibility Fixes for MASM32 (ML.EXE 14.x / VS 2022):

**Fixed Logical Expressions in Control-Flow Directives (A2154):**
- Resolved syntax errors in .if blocks where logical NOT (!) had ambiguous priority.
- Example: Changed !len2 == 1 to the explicit len2 != 1.

**Resolved Operand Size Mismatches (A2022):**
- Added explicit type casting using byte ptr and dword ptr to satisfy the strict type-checking of modern MASM.
- Example: Modified mov al, [esi] to mov al, byte ptr [esi] to prevent parser ambiguity.

**Fixed Constant Expression Magnitude Errors (A2071):**
- Replaced signed -1 with unsigned 0FFFFFFFFh in bitwise XOR operations to prevent sign-extension overflow.
- Example: Changed -1 xor WS_POPUP to 0FFFFFFFFh xor WS_POPUP.

**Circumvented Implicit Type Conflicts in Registers:**
- Replaced inc esi with add esi, 1 in procedures where ESI was previously associated with a structure via ASSUME.
- This prevents the "instruction operands must be the same size" error when a register is treated as a typed pointer.

**Resolved Local Variable Name Collisions:**
- Identified and fixed cases where LOCAL variable names conflicted with global macros or reserved symbols, which caused silent parser desynchronization.
