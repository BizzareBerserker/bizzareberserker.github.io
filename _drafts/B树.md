---
layout: post
title: "B树"
tag: dsa
category: essay
---
### B树的定义

B树$T$满足以下性质：

1. 每个结点$x$有以下属性：

   **a.** $x.n$: 存储在$x$中的关键字个数

   **b.** $x.key_1, x.key_2, \cdots, x.key_{x.n}$: n个关键字本身，满足$x.key_1\le x.key_2\le\cdots\le x.key_{x.n}$

   **c.** $x.leaf$: 如果$x$为叶结点则为TRUE, 否则为FALSE

   **d.** 对于内部节点$x$，包含$x.c_1, x.c_2,\cdots,x.c_{x.n+1}$: 指向其孩子的指针

2. $x.key_i$对子树根节点的关键字进行分隔：若$k_i$是$x.c_i$为根的子树的任一关键字，则

$$
k_1\le x.key_1\le k_2\le x.key_2\le\cdots\le x.key_{x.n}\le k_{x.n+1}
$$

3. 所有叶结点的高度相同，为树高$h$

4. B树的最小度数$t$用来衡量每个结点关键字数量的上下界：($t\ge 2$)

   **a.** 除了根节点的每个结点至少有$t-1$个关键字($t$个孩子)。非空树$T.root$至少有1个关键字

   **b.**每个结点最多有$2t-1$个关键字($2t$个孩子)。当一个内部结点恰好有$2t-1$个关键字时称该节点为**满的**(full)。

### B树的高度

若$n\ge1$, 则对任意一棵包含$n$个关键字，高度为$h$，最小度数$t\ge2$的B树$T$，有
$$
h\le\log_t\frac{n+1}{2}
$$

### B树的基本操作

搜索B树

```
B-TREE-SEARCH(x, k) {
	i = 1
	while i <= x.n and k >x.key[i]
		i = i + 1
	if i <= x.n and and k == x.key[i]
		return (x, i)
	else if x.leaf
		return NIL
	else
		DISK-READ(x, c[i])
		return B-TREE-SEARCH(x.c[i], k)
}
```

创建空B树

```
B-TREE-CREATE(T) {
	x = ALLOCATE-NODE()
	x.n = 0
	x.leaf = TRUE
	DISK-WRITE(x)
	T.root = x
}
```

分裂B树中的结点

```
B-TREE-SPLIT-CHILD(x, i) {
	y = x.c[i]
	z = ALLOCATE-NODE()
	z.leaf = y.leaf
	z.n = t - 1
	for j = 1 to t - 1
		z.key[j] = y.key[t + j]
	if not y.leaf
		for j = 1 to t
			z.c[j] = y.c[j + t]
	y.n = t -- 1
	for j = x.n + 1 downto i + 1
		x.c[j + 1] = x.c[j]
	x.c[i + 1] = z
	for j = x.n downto i
		x.key[j + 1] = x.key[j]
	x.key[i] = y.key[t]
	x.n = x.n + 1
	DISK-WRITE(y)
	DISK-WRITE(z)
	DISK-WRITE(x)
}
```

向B树中插入关键字

```
B-TREE-INSERT(T, k) {
	r = T.root
	if r.n == 2*t - 1
		s = ALLOCATE-NODE()
		T.root = s
		s.leaf = FALSE
		s.n = 0
		s.c[1] = r
		B-TREE-SPLIT-CHILD(s, 1)
		B-TREE-INSERT-NONFULL(s, k)
	else
		B-TREE-INSERT-NONFULL(r, k)
}
```

辅助的递归过程

```
B-TREE-INSERT-NONFULL(x, k) {
	i = x.n
	if x.leaf
		while i >= 1 and k < x.key[i]
			x.key[i + 1] = x.key[i]
			i = i - 1
		x.key[i + 1] = k
		x.n = x.n + 1
		DISK-WRITE(x)
	else
		while i >= 1 and k < x.key[i]
			i = i - 1
		i = i + 1
		DISK-READ(x, c[i])
		if x.c[i].n == 2*t - 1
			B-TREE-SPLIT-CHILD(x, i)
			if k > x.key[i]
				i = i + 1
		B-TREE-INSERT-NONFULL(x.c[i], k)
}
```

Segmentation Fault. 
