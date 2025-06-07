


✅ Minimal Linker Script (`linker.ld`)

ld
ENTRY(_start)

SECTIONS {
  Place .text in Flash at address 0x00000000 
  .text 0x00000000 : {
    (.text)
  }

  Place .data in SRAM at address 0x10000000 
  .data 0x10000000 : {
    (.data)
  }

  Place .bss after .data in SRAM 
  .bss : {
    (.bss)
    (COMMON)
  }
}


 📌 Explanation: Flash vs. SRAM Address Separation

| Section          | Typical Location         | Reason                                                                                     |
| ---------------- | ------------------------ | ------------------------------------------------------------------------------------------ |
| .text        | Flash(`0x00000000`) | Contains program instructions — non-volatile storage (doesn’t get erased on power off).    |
| .data / .bss | SRAM*(`0x10000000`) | Holds initialized (data) and uninitialized (bss) variables — needs fast read/write access.|

🔍 Why are addresses split?

Flash (ROM) is:

  Non-volatile (retains code after reset)
  Typically **read-only during runtime**
  Slower to write** and used mainly for **code**

SRAM is:

 Volatile(clears after reset)
 Fast and writable**, used for variables (`.data`, `.bss`)

> During boot, the startup code (like `crt0.S`) usually **copies initialized `.data` from Flash to SRAM**, and zeroes `.bss`.


 🧠 Bonus Tip: RV32IMC Constraints

RV32IMC (32-bit, Integer, Multiply, Compressed):

  Alignment matters for performance (instructions must be 2-byte aligned, ideally 4-byte aligned).
  You can add ALIGN(4); directives if needed for strict alignment in Flash or RAM.


