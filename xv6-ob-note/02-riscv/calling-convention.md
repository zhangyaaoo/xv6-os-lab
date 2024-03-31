# 函数调用的六个步骤

Similarly, in the execution of a procedure, the program must follow these six steps:
1. Put parameters in a place where the procedure can access them.
2. Transfer control to the procedure.
3. Acquire the storage resources needed for the procedure.
4. Perform the desired task.
5. Put the result value in a place where the calling program can access it.
6. Return control to the point of origin, since a procedure can be called from several points in a program.


RISCV中，寄存器的使用约定：详见 [riscv-calling](01-docs/riscv-calling.pdf)

**t0 - t6：** temporary registers that are not preserved by the callee (called procedure) on a procedure call.

**s0 - s11：** saved registers that must be preserved on a procedure call (if used, the callee saves and restores them).

The caller does not expect the temporary registers to be preserved across a procedure call.

The callee must assume that the caller needs the saved registers's value.  So, the callee must save and restore the saved register, if callee used.

# Caller Saved Register

示例代码一：
```C
void foo(void)
{
	// :
	// 使用了 t0 - t6
	// :

	bar();

	// :
	// 又使用到了 t0 - t6
	// :
}
```

上面的示例代码中，作为 Caller 的 foo() 在调用函数 bar() 后，再次使用临时寄存器时，就不能假定临时寄存器中的值还是调用 bar() 之前的值。

如果 foo() 在调用 bar() 之前给临时寄存器赋的值，在 bar() 调用后，还需要使用，那么需要 foo() 自己处理保存和恢复的工作。

**所以**，t0 - t6 属于 `Caller Saved Register`。

同样属于 `Caller Saved Register` 的寄存器还有 a0 - a7 和 ra。

函数中不再调用其他函数的函数称为叶子函数。叶子函数中，因为不再调用其他函数，ra 的值不会改变，就可以不用处理 ra 的保存和恢复。

# Callee Saved Register

示例代码二：
```C
void foo(void)
{
	// :
	// 使用了s0-s11
	// :

	bar();

	// :
	// 又使用到了s0-s11
	// :
}
```

上面的示例代码中，作为 Caller 的 foo() 在调用函数 bar() 后，就能放心的再次使用保存寄存器中的值，并且能认为保存寄存器中的值还是调用 bar() 之前的值。

因为作为 Callee 的函数 bar() 中，如果使用到了保存寄存器(s0 - s11)，它需要保证在函数 bar() 执行前后，保存寄存器中的值不变。即，在使用前保存，使用后恢复。

**所以**，s0 - s11 属于 `Callee Saved Register`。



# 栈帧的形成






***参考：***
1. Computer Organization and Design RISC-V edition.pdf