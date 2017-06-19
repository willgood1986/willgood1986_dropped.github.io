---
title: Bubble in sort methods
date: 2017-03-08 15:23:38
tags: Sort, Order, Bubble, Python
categories: SortMethods
---

> Bubble sort is a basic sort method. Here is a optimized version

<!--more-->

```bash
def bubble(src):
    flag = True
    while flag:
        flag = False
        maxlen = len(src)
        for i in range(1, maxlen):
            if src[i - 1] > src[i]:
                src[i - 1], src[i] =src[i], src[i - 1]
                flag = True
        maxlen -= 1

```
