---
layout: post
title: Python Thread
subtitle: Python Thread
categories: python
tags: [python]
---

# Python thread

用threading模組執行多執行緒（multithreading）的平行化程式

```Python
import threading
import time

# 子執行緒的工作函數
def job():
  for i in range(5):
    print("Child thread:", i)
    time.sleep(1)

# 建立一個子執行緒
t = threading.Thread(target = job)

# 執行該子執行緒
t.start()

# 主執行緒繼續執行自己的工作
for i in range(3):
  print("Main thread:", i)
  time.sleep(1)

# 等待 t 這個子執行緒結束
t.join()

print("Done.")
```

- 建立執行緒
threading.Thread(target=**function**, name="Thread名字", args=參數)

- 開始執行緒

\<Thread\>.start()

- 主執行緒暫停，等待指定的執行緒結束，join 前面要放指定的執行緒名稱，timeout為thread最大運行時間

\<Thread\>.join(**timeout**)

- 查看目前有多少個執行緒

\<Thread\>.active_count()

- 查看目前使用執行緒的資訊

\<Thread\>.enumerate()

- 查看目前在哪個執行緒中

\<Thread\>.current_thread()

- 主執行緒執行完畢後，不管其他的Thread是否已執行完畢，都強制跟主執行緒一起結束，必須寫在start() 之前，預設為 False

\<Thread\>.setDaemon()

## 物件導向

```Python
import threading
import time

# 子執行緒類別
class MyThread(threading.Thread):
  def __init__(self, num):
    threading.Thread.__init__(self)
    self.num = num

  def run(self):
    print("Thread", self.num)
    time.sleep(1)

# 建立 5 個子執行緒
threads = []
for i in range(5):
  threads.append(MyThread(i))
  threads[i].start()

# 主執行緒繼續執行自己的工作
# ...

# 等待所有子執行緒結束
for i in range(5):
  threads[i].join()

print("Done.")
```

threading.Thread 在開始執行時，會呼叫它自己的 run 方法函數

Reference:

<https://blog.gtwang.org/programming/python-threading-multithreaded-programming-tutorial/>

<https://medium.com/ching-i/%E5%A4%9A%E5%9F%B7%E8%A1%8C%E7%B7%92-python-threading-52e1dfb3d5c9>