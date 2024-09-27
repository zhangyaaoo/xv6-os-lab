---
annotation-target: Docs/book-riscv-rev3.pdf
---


>%%
>```annotation-json
>{"created":"2024-05-29T14:32:36.601Z","text":"文件系统中的数据是持久保存的数据, 是掉电保存的数据.\n\n文件系统中不仅要保存数据本身, 还要保存一些数据结构, 包括文件和目录的路径, 文件内容在哪些块上, 和哪些块是使用或者空闲的.\n\n文件系统需要支持故障恢复, 比如意外掉电, 重启后文件系统要能够正常工作.\n\n文件系统要支持并发. 要支持常用块的缓存.","updated":"2024-05-29T14:32:36.601Z","document":{"title":"xv6: a simple, Unix-like teaching operating system","link":[{"href":"urn:x-pdf:0f3a5bcdfa474cb022f66cfa7b2b1580"},{"href":"vault:/xv6-ob-note/01-docs/book-riscv-rev3.pdf"}],"documentFingerprint":"0f3a5bcdfa474cb022f66cfa7b2b1580"},"uri":"vault:/xv6-ob-note/01-docs/book-riscv-rev3.pdf","target":[{"source":"vault:/xv6-ob-note/01-docs/book-riscv-rev3.pdf","selector":[{"type":"TextPositionSelector","start":206870,"end":206914},{"type":"TextQuoteSelector","exact":"The file system addresses several challenges","prefix":" a virtio disk for persistence. ","suffix":":• The file system needs on-disk"}]}]}
>```
>%%
>*%%PREFIX%%a virtio disk for persistence.%%HIGHLIGHT%% ==The file system addresses several challenges== %%POSTFIX%%:• The file system needs on-disk*
>%%LINK%%[[#^wfnhem0r3o|show annotation]]
>%%COMMENT%%
>文件系统中的数据是持久保存的数据, 是掉电保存的数据.
>
>文件系统中不仅要保存数据本身, 还要保存一些数据结构, 包括文件和目录的路径, 文件内容在哪些块上, 和哪些块是使用或者空闲的.
>
>文件系统需要支持故障恢复, 比如意外掉电, 重启后文件系统要能够正常工作.
>
>文件系统要支持并发. 要支持常用块的缓存.
>%%TAGS%%
>#文件系统
^wfnhem0r3o
