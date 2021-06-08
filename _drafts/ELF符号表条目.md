---
layout: post
title: "ELF符号表条目"
tag: linux
category: essay
---

`.symtab`节中包含ELF符号表。这张表是一个符号表条目的数组。每个条目的格式如下：

```c
typedef struct {
    int name;			/* String table offset */
    char type:4,		/* Function or data (4 bits) */
    	 binding: 4; 	/* Local or global (4 bits) */
    char reserved;		/* Unused */
    short section;		/* Section header index */
    long value;			/* Section offset or absolute address */
    long size;			/* Object size in bytes */
} Elf64_Symbol;
```

