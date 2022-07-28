---
layout: post
title: Python Queue
subtitle: Python Queue
categories: python
tags: [python]
---

# Python Queue

適用於多執行緒中的資訊交換

```Python
import queue
```

## Queue種類

- queue.Queue：FIFO 先進先出
- queue.LifoQueue：LIFO類似於堆疊 stack，即先進後出
- queue.PriorityQueue：優先級別越低越先出來

## Queue成員函式

Queue.qsize()：返回 Queue 的大小
Queue.empty()：如果 Queue 為空，返回 True，反之返回 False
Queue.full()：如果 Queue 滿了，返回 True，反之返回 False
Queue.get([block[, timeout]])：取出 Queue，timeout 可以指定等待時間
Queue.get_nowait()：等於 Queue.get(False)
Queue.put(item)：放入 Queue，timeout 可以指定等待時間
Queue.put_nowait(item)：等於 Queue.put(item, False)
Queue.task_done()：在完成一項工作之後，Queue.task_done() 向任務已經完成的 Queue 發送一個訊號
Queue.join()：等待直到 Queue 為空，再繼續執行

```Python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
import queue

q = queue.Queue()

q.put(1)
q.put(2)
q.put(3)

print(q.empty())
print(q.get())
print(q.get())
print(q.get())
print(q.empty())
```

## Queue Size

- 設定Queue的maxsize

Queue(maxsize=3)

Queue滿了之後要 put 會 block，改成 q.put(i, block=False) 的話就不會 block

Reference:

<https://shengyu7697.github.io/python-queue/>
