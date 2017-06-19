---
title: Insert Order in Sort Methods
date: 2017-03-09 05:30:07
tags: Sort, Order, Insert, Python
categories: SortMethods
---

> Insert order method is kind of reverse version of Bubble

<!--more-->

### Import tips
Insert order starts from the second item, check and swap to make sure
the last item is inserted at the proper position

### Code Block

```bash
def insert(src):
    # Start from the second one
    for i in range(1, len(src)):
        left = i - 1
        # Check and add the last one into a proper pos, by compare
        # Makre sure all indexes, just less than i
        leftindexes = list(range(left + 1))[::-1]
        for j in leftindexes:
            if src[j] > src[j + 1]:
                src[j], src[j + 1] = src[j + 1], src[j]
```
