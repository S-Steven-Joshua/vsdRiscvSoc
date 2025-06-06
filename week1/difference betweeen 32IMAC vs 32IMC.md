| Letter       | Stands For                 | Description                                                                                                                    |
| ------------ | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| I       | Integer                    | Base integer instructions (add, sub, load, store, etc.)                                                                             |
| M       | Multiply/Divide            | Instructions like `mul`, `div`, `rem`, etc.                                                                                         |
| A       | **Atomic**                 | Instructions for atomic read-modify-write (e.g. `amoadd.w`, `lr.w`, `sc.w`) — essential for multithreading and synchronization      |
| C       | Compressed                 | 16-bit compressed instructions to reduce code size                                                                                  |
| Zicsr  | Control & Status Registers | Used for privileged instructions like reading/writing CSRs                                                                           |
| Zifencei| Instruction Fences         | For ordering instruction fetches in multi-core scenarios                                                                            |
______________________________________________________________________________________________________________________________________________________________________________



| ISA Variant | Includes                                            | Usage Scenario                                                                        |
| ----------- | --------------------------------------------------- | ------------------------------------------------------------------------------------- |
| RV32IMAC  | Integer + Multiply/Divide + **Atomic** + Compressed | Suitable for **multithreaded programs** or any app needing atomic operations          |
| RV32IMC   | Integer + Multiply/Divide + Compressed (no Atomic)  | Good for **bare-metal apps**, or where atomicity is not needed (e.g. single-threaded) |
