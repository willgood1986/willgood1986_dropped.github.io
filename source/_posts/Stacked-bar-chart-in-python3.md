---
title: Stacked bar chart in python3
date: 2017-02-26 07:32:26
tags: chart, matplotlib
categories: python
---

> We can use matplotlib to draw some charts   

<!--more-->

### Install matplotlib in python3

> There is a package named with python3-matplotlib, we can use apt-get to install

### Draw a basic stacked bar chart in python3

```
import numpy as np
import matplotlib.pyplot as plt

N = 5
menMeans = (20, 35, 30, 35, 27)
womenMeans = (0, 32, 34, 20, 25)
menStd =(5, 8, 4, 1, 2)
womenStd=(1, 0, 1, 3, 3)
ind = np.arange(N)
width = 0.35

p1 = plt.bar(ind, menMeans, width, color='green', yerr=menStd)
p2 = plt.bar(ind, womenMeans, width, color='red', bottom=menMeans, yerr=womenStd)

plt.ylabel('Task Progress')
plt.title('Task progress group by item')
plt.xticks(ind, ('G1', 'G2', 'G3', 'G4', 'G5'))
plt.yticks(np.arange(0, 80, 10))
plt.legend((p1[0], p2[0]), ('Finished', 'UnFinished'))
plt.savefig('/home/rainy/myfirststackedimage.jpg')
plt.show()

```
