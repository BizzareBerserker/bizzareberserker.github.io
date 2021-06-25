---
layout: post
title: "Mark&Sweep垃圾收集器"
tag: C
category: essay
---

Mark&Sweep垃圾收集器由标记阶段和清除阶段构成。标记阶段标记根节点所有可达的和已分配的后继，而后面的清除阶段释放每个未被标记的已分配块。

`mark`阶段：

```c
void mark(ptr p) {
    if ((b = isPtr(p)) == NULL)
        return;
    if (blockMarked(b))
        return;
    markBlock(b);
    len = length(b);
    for (i = 0; i < len; i++)
        mark(b[i]);
    return;
}
```

`sweep`阶段：

```c
void sweep(ptr b, ptr end) {
    while (b < end) {
        if (blockMarked(b))
            unmarkBlock(b);
        else if (blockAllocated(b))
            free(b);
        b = nextBlock(b);
    }
    return;
}
```

