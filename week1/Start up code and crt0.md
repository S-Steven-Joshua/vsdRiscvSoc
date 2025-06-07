

## ✅ What `crt0.S` Typically Does

Here’s what it **usually includes**, step by step:

### 1. **Set up the stack pointer (`sp`)**

* Allocates a known-good RAM location as the top of the stack.
* Stack is essential for calling functions and using local variables.

```assembly
la sp, _stack_top
```

---

### 2. **Zero the `.bss` section**

* `.bss` holds uninitialized global/static variables — they must be zero-initialized.

```assembly
la a0, __bss_start
la a1, __bss_end
loop:
  bge a0, a1, done
  sw zero, 0(a0)
  addi a0, a0, 4
  j loop
done:
```

---

### 3. **Copy `.data` section from Flash to RAM**

* `.data` holds **initialized variables**, stored in Flash but used in RAM.

```assembly
la a0, _data_lma   # Load Memory Address in Flash
la a1, _data_start # Virtual Address in RAM
la a2, _data_end
copy_loop:
  bge a1, a2, copy_done
  lw t0, 0(a0)
  sw t0, 0(a1)
  addi a0, a0, 4
  addi a1, a1, 4
  j copy_loop
copy_done:
```

---

### 4. **Call `main()`**

```assembly
call main
```

---

### 5. **Handle exit — infinite loop**

```assembly
1:  j 1b  # Loop forever if main() returns
```

---

## 📦 Where Do You Get a `crt0.S`?

### ✅ 1. **From Newlib (Embedded C Library)**

* Look inside:
  `/newlib/libc/machine/riscv/crt0.S`
  or search GitHub:
  [`riscv crt0.S site:newlib.org`](https://github.com/search?q=riscv+crt0.S+newlib)

### ✅ 2. **From SiFive or Platform SDKs**

* **Freedom E SDK** (SiFive):
  Contains board-specific `crt0.S` and linker scripts.

  GitHub: [https://github.com/sifive/freedom-e-sdk](https://github.com/sifive/freedom-e-sdk)

### ✅ 3. **Minimal Template Example**

You can also write your own minimal version based on what's listed above.

---

## 🔁 Summary Table

| Step          | Purpose                                 |
| ------------- | --------------------------------------- |
| Set `sp`      | Prepare stack                           |
| Clear `.bss`  | Ensure uninitialized variables are zero |
| Copy `.data`  | Move init data from Flash to RAM        |
| Call `main()` | Start C program                         |
| Loop forever  | Prevent return to unknown address       |



