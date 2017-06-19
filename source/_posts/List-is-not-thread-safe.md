---
title: List is not thread safe
date: 2017-04-21 05:42:03
tags: Multi-Thread
Categories:
   - C#
---

> There are more than one steps when trying to add an item into the list.Allocate space, adjust index,etc.List.add(item) is not an atomatic operation.

<!--more-->

### Source codes

```bash
private static void Test()
		{
			const Int32 MaxCount = 10000000;

			var counter = 0;

			var semaphere = new System.Threading.Semaphore(8, 8);
			var locker = new Object();

			var nums = new List<Int32>();

			for (var i = 0; i < MaxCount; i++)
			{
				Task.Factory.StartNew(
					() =>
					{
						if (semaphere.WaitOne(5 * 60 * 1000))
						{
							try
							{

								//lock (locker)
								{
									nums.Add(i);
								}
								Interlocked.Increment(ref counter);
							}
							finally
							{
								semaphere.Release();
							}
						}
					});
			}

			while (counter < MaxCount)
			{
				Thread.Sleep(500);
			}

			Console.WriteLine("Item count in list expected:{0}, actual:{1}", MaxCount, nums.Count);

		}
```
