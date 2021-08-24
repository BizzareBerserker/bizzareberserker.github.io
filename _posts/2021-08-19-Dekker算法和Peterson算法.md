---
layout: post
title: "Dekker算法和Peterson算法"
tag: os
category: essay
---

## 其他算法

### 单标志法

```c
int turn;

void P0() {
    while (turn != 0);
    /* critical section */;
    turn = 1;
    /* remainder */;
}

void P1() {
    while (turn != 1);
    /* critical section */;
    turn = 0;
    /* remainder */;
}
```

### 双标志先检查法

```c
bool flag[2];

void P0() {
    while (flag[1]);
    flag[0] = true;
    /* critical section */
    flag[0] = false;
    /* remainder */
}

void P1() {
    while (flag[0]);
    flag[1] = true;
    /* critical section */
    flag[1] = false;
    /* remainder */
}
```

### 双标志后检查法

```c
bool flag[2];

void P0() {
    flag[0] = true;
    while (flag[1]);
    /* critical section */;
    flag[0] = false;
    /* remainder */;
}
```

## Dekker算法

Dijkstra给出了一种实现两个进程互斥的算法，该算法由Dekker设计：

```c
bool flag[2];
int turn;

void P0() {
    while (true) {
        flag[0] = true;
        while (flag[1]) {
            if (turn == 1) {
                flag[0] = false;
                while (turn == 1); /* do nothing*/
                flag[1] = true;
            }
        }
        /* critical section */
        turn = 1;
        flag[0] = false;
        /* remainder */
    }
} 

void P1() {
    while (true) {
        flag[1] = true;
        while (flag[0]) {
            if (turn == 0) {
                flag[1] = false;
                while (turn == 0); 	/* do nothing */
                flag[1] = true;
            }
        }
        /* critical section */
        turn = 0;
        flag[1] = false;
        /* remainder */
    }
}

void main() {
    flag[0] = false;
    flag[1] = false;
    turn = 1;
    parbegin(P0, P1);
}
```

其中：`turn`表示哪个变量有权进入临界区，`flag`标志哪个变量试图有意愿进入临界区，`parbegin`表示并行开始几个子程序。

## Peterson算法

Peterson算法给出了一种更为简单的方法解决两个进程的互斥问题，该方法可以轻松推广到多进程的情况。

```c
bool flag[2];
int turn;

void P0() {
    while (true) {
        flag[0] = true;
        turn = 1;
        while (flag[1] && turn == 1);   /* do nothing */
        /* critical section */
        flag[0] = false;
        /* remainder */
    }
}

void P1() {
    while (true) {
        flag[1] = true;
        turn = 0;
        while (flag[0] && turn == 0);    /* do nothing */
        /* critical section */
        flag[1] = false;
        /* remainder */
    }
}

void main() {
    flag[0] = false;
    flag[1] = false;
	parbegin(P0, P1);
}
```

