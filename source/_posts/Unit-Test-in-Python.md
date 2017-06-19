---
title: Unit Test in Python
date: 2017-03-08 15:32:10
tags: ut, unittest, testcase
categories: UnitTest
---

> UT is a standard and important part in development.
Here is a sample of UT in Python3

<!--more-->

### Some concepts
1. module - unittest
2. Test class inherites from unittest.TestCase
3. All testcases are instance methods
4. use TestCase.assertXXXX method to assert result
5. use unittest.main() to run testcases

### Codes

```bash
import unittest
from orders import bubble

class MyTest(unittest.TestCase):
    def bubble_normal(self):
        src = [1,4,2,8,6,5]
        bubble.bubble(src)
        for x in range(1, len(src)):
            self.assertTrue(src[x - 1] < src[x])


if __name__ == '__main__':
    unittest.main()

```
