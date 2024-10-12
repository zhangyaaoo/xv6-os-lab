---
annotation-target: Docs/riscv-privileged-20211203.pdf
---








>%%
>```annotation-json
>{"text":"sstatus 反映的是 mstatus 的子集，部分位域只有 mstatus 有。\n\n类似的还有 sip 和 sie，分别是 mip 和 mie 视图的子集。","target":[{"source":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":61899,"end":61979},{"type":"TextQuoteSelector","exact":"A restricted view of mstatus appears as the sstatus register in the S-level ISA.","prefix":"hart’s currentoperating state.","suffix":"31 30 23 22 21 20 19 18 17SD WPR"}]}],"created":"2024-04-15T15:11:51.759Z","updated":"2024-04-15T15:11:51.759Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}
>```
>%%
>*%%PREFIX%%hart’s currentoperating state.%%HIGHLIGHT%% ==A restricted view of mstatus appears as the sstatus register in the S-level ISA.== %%POSTFIX%%31 30 23 22 21 20 19 18 17SD WPR*
>%%LINK%%[[#^3ii812sem5d|show annotation]]
>%%COMMENT%%
>sstatus 反映的是 mstatus 的子集，部分位域只有 mstatus 有。
>
>类似的还有 sip 和 sie，分别是 mip 和 mie 视图的子集。
>%%TAGS%%
>#mstatus, #sstatus
^3ii812sem5d


>%%
>```annotation-json
>{"created":"2024-04-15T15:28:57.681Z","text":"比如：当 hart 在 M-mode 下运行时，无论 SIE 如何设置，S-mode 下的中断总是禁用的。即：中断不会打断高特权级的流程转而到低特权级执行。","updated":"2024-04-15T15:28:57.681Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","target":[{"source":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":63527,"end":63676},{"type":"TextQuoteSelector","exact":"Interrupts for lower-privilege modes, w<x, are always globallydisabled regardless of the setting of any global w IE bit for the lower-privilege mode.","prefix":"dglobally disabled when x IE=0. ","suffix":" Interrupts forhigher-privilege "}]}]}
>```
>%%
>*%%PREFIX%%dglobally disabled when x IE=0.%%HIGHLIGHT%% ==Interrupts for lower-privilege modes, w<x, are always globallydisabled regardless of the setting of any global w IE bit for the lower-privilege mode.== %%POSTFIX%%Interrupts forhigher-privilege*
>%%LINK%%[[#^qwwnqisn90m|show annotation]]
>%%COMMENT%%
>比如：当 hart 在 M-mode 下运行时，无论 SIE 如何设置，S-mode 下的中断总是禁用的。即：中断不会打断高特权级的流程转而到低特权级执行。
>%%TAGS%%
>#SIE
^qwwnqisn90m


>%%
>```annotation-json
>{"created":"2024-04-15T15:34:02.593Z","text":"比如：当 hart 在 S-mode 下运行时，无论 MIE 如何设置，M-mode 下的中断总是启用的。即：在低特权级运行时，不能禁止高特权级的中断。","updated":"2024-04-15T15:34:02.593Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","target":[{"source":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":63677,"end":63827},{"type":"TextQuoteSelector","exact":"Interrupts forhigher-privilege modes, y>x, are always globally enabled regardless of the setting of the global y IEbit for the higher-privilege mode. ","prefix":"t for the lower-privilege mode. ","suffix":"Higher-privilege-level code can "}]}]}
>```
>%%
>*%%PREFIX%%t for the lower-privilege mode.%%HIGHLIGHT%% ==Interrupts forhigher-privilege modes, y>x, are always globally enabled regardless of the setting of the global y IEbit for the higher-privilege mode.== %%POSTFIX%%Higher-privilege-level code can*
>%%LINK%%[[#^l05b6vd4wa8|show annotation]]
>%%COMMENT%%
>比如：当 hart 在 S-mode 下运行时，无论 MIE 如何设置，M-mode 下的中断总是启用的。即：在低特权级运行时，不能禁止高特权级的中断。
>%%TAGS%%
>#SIE
^l05b6vd4wa8


>%%
>```annotation-json
>{"text":"例如：\nU-mode 陷入到 S-mode 时：\n1. SPIE 设置为 SIE 的值；\n2. SIE 设置为 0；\n3. SPP 设置为 U-mode。","target":[{"source":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":64614,"end":64752},{"type":"TextQuoteSelector","exact":"When a trap is takenfrom privilege mode y into privilege mode x, x PIE is set to the value of x IE; x IE is set to 0; andx PP is set to y.","prefix":"s wide and SPP is one bit wide.","suffix":"For lower privilege modes, any t"}]}],"created":"2024-04-15T15:41:44.755Z","updated":"2024-04-15T15:41:44.755Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}
>```
>%%
>*%%PREFIX%%s wide and SPP is one bit wide.%%HIGHLIGHT%% ==When a trap is takenfrom privilege mode y into privilege mode x, x PIE is set to the value of x IE; x IE is set to 0; andx PP is set to y.== %%POSTFIX%%For lower privilege modes, any t*
>%%LINK%%[[#^saj3hltzjm9|show annotation]]
>%%COMMENT%%
>例如：
>U-mode 陷入到 S-mode 时：
>1. SPIE 设置为 SIE 的值；
>2. SIE 设置为 0；
>3. SPP 设置为 U-mode。
>%%TAGS%%
>#TRAP, #陷阱
^saj3hltzjm9


>%%
>```annotation-json
>{"text":"例如：\nU-mode 陷入到 S-mode 处理完成后，执行 sret 时：\n1. SIE 设置为 SPIE 的值；\n2. Hart 的特权级从 S-mode 切换到 U-mode，因为 SPP 为 U-mode；\n3. SPIE 设置为 1；\n4. SPP 设置为支持的最小特权模式；\n5. 如果 SPP 不是 M-mode，sret 执行后，MPRV 会设置为 0；","target":[{"source":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":65249,"end":65522},{"type":"TextQuoteSelector","exact":"When executing an x RET instruction, supposing x PP holds the value y, x IE is set to x PIE; theprivilege mode is changed to y; x PIE is set to 1; and x PP is set to the least-privileged supportedmode (U if U-mode is implemented, else M). If x PP̸=M, x RET also sets MPRV=0","prefix":"n M-mode or S-mode respectively.","suffix":".Setting xPP to the least-privil"}]}],"created":"2024-04-15T15:55:24.646Z","updated":"2024-04-15T15:55:24.646Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}
>```
>%%
>*%%PREFIX%%n M-mode or S-mode respectively.%%HIGHLIGHT%% ==When executing an x RET instruction, supposing x PP holds the value y, x IE is set to x PIE; theprivilege mode is changed to y; x PIE is set to 1; and x PP is set to the least-privileged supportedmode (U if U-mode is implemented, else M). If x PP̸=M, x RET also sets MPRV=0== %%POSTFIX%%.Setting xPP to the least-privil*
>%%LINK%%[[#^b58py1eeybt|show annotation]]
>%%COMMENT%%
>例如：
>U-mode 陷入到 S-mode 处理完成后，执行 sret 时：
>1. SIE 设置为 SPIE 的值；
>2. Hart 的特权级从 S-mode 切换到 U-mode，因为 SPP 为 U-mode；
>3. SPIE 设置为 1；
>4. SPP 设置为支持的最小特权模式；
>5. 如果 SPP 不是 M-mode，sret 执行后，MPRV 会设置为 0；
>%%TAGS%%
>#TRAP, #陷阱
^b58py1eeybt


>%%
>```annotation-json
>{"created":"2024-04-15T16:03:48.331Z","text":"xPP 中保存的特权级模式只可能是当前特权级或者更低特权级模式。","updated":"2024-04-15T16:03:48.331Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","target":[{"source":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":65724,"end":65835},{"type":"TextQuoteSelector","exact":"x PP fields are WARL fields that can hold only privilege mode x and any implemented privilegemode lower than x.","prefix":"ivileged Architectures V20211203","suffix":" If privilege mode x is not impl"}]}]}
>```
>%%
>*%%PREFIX%%ivileged Architectures V20211203%%HIGHLIGHT%% ==x PP fields are WARL fields that can hold only privilege mode x and any implemented privilegemode lower than x.== %%POSTFIX%%If privilege mode x is not impl*
>%%LINK%%[[#^n7ncjbligt|show annotation]]
>%%COMMENT%%
>xPP 中保存的特权级模式只可能是当前特权级或者更低特权级模式。
>%%TAGS%%
>#MPP, #SPP
^n7ncjbligt


>%%
>```annotation-json
>{"created":"2024-04-15T16:18:51.636Z","updated":"2024-04-15T16:18:51.636Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","target":[{"source":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":125702,"end":125803},{"type":"TextQuoteSelector","exact":"The interrupt will only be taken if interruptsare enabled and the MTIE bit is set in the mie register","prefix":" a result of writing mtimecmp). ","suffix":".Volume II: RISC-V Privileged Ar"}]}]}
>```
>%%
>*%%PREFIX%%a result of writing mtimecmp).%%HIGHLIGHT%% ==The interrupt will only be taken if interruptsare enabled and the MTIE bit is set in the mie register== %%POSTFIX%%.Volume II: RISC-V Privileged Ar*
>%%LINK%%[[#^bzrr132ookr|show annotation]]
>%%COMMENT%%
>
>%%TAGS%%
>
^bzrr132ookr


>%%
>```annotation-json
>{"text":"RISC-V特权级的定义","target":[{"source":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":27626,"end":27649},{"type":"TextQuoteSelector","exact":"RISC-V privilege levels","prefix":"eserved3 11 Machine MTable 1.1:","suffix":".exception to be raised. These e"}]}],"created":"2024-04-15T23:46:01.102Z","updated":"2024-04-15T23:46:01.102Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}
>```
>%%
>*%%PREFIX%%eserved3 11 Machine MTable 1.1:%%HIGHLIGHT%% ==RISC-V privilege levels== %%POSTFIX%%.exception to be raised. These e*
>%%LINK%%[[#^9tv75xldabn|show annotation]]
>%%COMMENT%%
>RISC-V特权级的定义
>%%TAGS%%
>
^9tv75xldabn


>%%
>```annotation-json
>{"created":"2024-04-16T00:01:09.522Z","text":"默认情况下，所有的 trap 都是在 M-mode 下处理的。","updated":"2024-04-16T00:01:09.522Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","target":[{"source":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":90332,"end":90406},{"type":"TextQuoteSelector","exact":"By default, all traps at any privilege level are handled in machine mode, ","prefix":" Registers (medeleg and mideleg)","suffix":"though a machine-modehandler can"}]}]}
>```
>%%
>*%%PREFIX%%Registers (medeleg and mideleg)%%HIGHLIGHT%% ==By default, all traps at any privilege level are handled in machine mode,== %%POSTFIX%%though a machine-modehandler can*
>%%LINK%%[[#^1ln136m0p2o|show annotation]]
>%%COMMENT%%
>默认情况下，所有的 trap 都是在 M-mode 下处理的。
>%%TAGS%%
>#TRAP
^1ln136m0p2o


>%%
>```annotation-json
>{"created":"2024-04-16T00:06:57.502Z","text":"Trap 发生时，不会陷入到更低特权级的模式。","updated":"2024-04-16T00:06:57.502Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","target":[{"source":"vault:/xv6-ob-note/01-docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":92692,"end":93194},{"type":"TextQuoteSelector","exact":"Traps never transition from a more-privileged mode to a less-privileged mode. For example, if M-mode has delegated illegal instruction exceptions to S-mode, and M-mode software later executesan illegal instruction, the trap is taken in M-mode, rather than being delegated to S-mode. Bycontrast, traps may be taken horizontally. Using the same example, if M-mode has delegated illegalinstruction exceptions to S-mode, and S-mode software later executes an illegal instruction, the trapis taken in S-mode","prefix":"ay always add such restrictions.","suffix":".Delegated interrupts result in "}]}]}
>```
>%%
>*%%PREFIX%%ay always add such restrictions.%%HIGHLIGHT%% ==Traps never transition from a more-privileged mode to a less-privileged mode. For example, if M-mode has delegated illegal instruction exceptions to S-mode, and M-mode software later executesan illegal instruction, the trap is taken in M-mode, rather than being delegated to S-mode. Bycontrast, traps may be taken horizontally. Using the same example, if M-mode has delegated illegalinstruction exceptions to S-mode, and S-mode software later executes an illegal instruction, the trapis taken in S-mode== %%POSTFIX%%.Delegated interrupts result in*
>%%LINK%%[[#^uct0ipnn92|show annotation]]
>%%COMMENT%%
>Trap 发生时，不会陷入到更低特权级的模式。
>%%TAGS%%
>#TRAP
^uct0ipnn92


>%%
>```annotation-json
>{"created":"2024-10-11T12:56:00.791Z","text":"satp寄存器中MODE字段的定义","updated":"2024-10-11T12:56:00.791Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/Docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/Docs/riscv-privileged-20211203.pdf","target":[{"source":"vault:/Docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":200935,"end":200962},{"type":"TextQuoteSelector","exact":"Encoding of satp MODE field","prefix":"gnated for custom useTable 4.4: ","suffix":".operating systems [2]. Addition"}]}]}
>```
>%%
>*%%PREFIX%%gnated for custom useTable 4.4:%%HIGHLIGHT%% ==Encoding of satp MODE field== %%POSTFIX%%.operating systems [2]. Addition*
>%%LINK%%[[#^8yllwsgo0e4|show annotation]]
>%%COMMENT%%
>satp寄存器中MODE字段的定义
>%%TAGS%%
>
^8yllwsgo0e4


>%%
>```annotation-json
>{"created":"2024-10-11T13:14:44.263Z","text":"mstatus.TVM 字段可以用来拦截 S-mode 下对 satp 寄存器的读写操作，和拦截 SFENCE.VMA 、SINVAL.VMA指令的执行。","updated":"2024-10-11T13:14:44.263Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/Docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/Docs/riscv-privileged-20211203.pdf","target":[{"source":"vault:/Docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":74512,"end":74736},{"type":"TextQuoteSelector","exact":"When TVM=1, attempts to read or write the satp CSRor execute an SFENCE.VMA or SINVAL.VMA instruction while executing in S-mode will raise anillegal instruction exception. When TVM=0, these operations are permitted in S-mode.","prefix":"l-memory management operations. ","suffix":" TVM isread-only 0 when S-mode i"}]}]}
>```
>%%
>*%%PREFIX%%l-memory management operations.%%HIGHLIGHT%% ==When TVM=1, attempts to read or write the satp CSRor execute an SFENCE.VMA or SINVAL.VMA instruction while executing in S-mode will raise anillegal instruction exception. When TVM=0, these operations are permitted in S-mode.== %%POSTFIX%%TVM isread-only 0 when S-mode i*
>%%LINK%%[[#^w0dj6vt2j8a|show annotation]]
>%%COMMENT%%
>mstatus.TVM 字段可以用来拦截 S-mode 下对 satp 寄存器的读写操作，和拦截 SFENCE.VMA 、SINVAL.VMA指令的执行。
>%%TAGS%%
>#TVM
^w0dj6vt2j8a


>%%
>```annotation-json
>{"created":"2024-10-11T15:24:14.079Z","text":"PTE 权限控制位。","updated":"2024-10-11T15:24:14.079Z","document":{"title":"riscv-privileged-20211203.pdf","link":[{"href":"urn:x-pdf:3bbd00947260c6060c7c578a15048ab9"},{"href":"vault:/Docs/riscv-privileged-20211203.pdf"}],"documentFingerprint":"3bbd00947260c6060c7c578a15048ab9"},"uri":"vault:/Docs/riscv-privileged-20211203.pdf","target":[{"source":"vault:/Docs/riscv-privileged-20211203.pdf","selector":[{"type":"TextPositionSelector","start":216765,"end":216796},{"type":"TextQuoteSelector","exact":"encoding of the permission bits","prefix":"e use. Table 4.5 summarizes the ","suffix":".X W R Meaning0 0 0 Pointer to n"}]}]}
>```
>%%
>*%%PREFIX%%e use. Table 4.5 summarizes the%%HIGHLIGHT%% ==encoding of the permission bits== %%POSTFIX%%.X W R Meaning0 0 0 Pointer to n*
>%%LINK%%[[#^fgegg0dqk7n|show annotation]]
>%%COMMENT%%
>PTE 权限控制位。
>%%TAGS%%
>#PTE
^fgegg0dqk7n
