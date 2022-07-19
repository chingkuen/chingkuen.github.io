---
layout: post
title: Python Logging
subtitle: Python Logging
categories: python
tags: [python]
---

# Python Logging

## logging 等級

等級 | 等級數值 | 輸出函數 | 說明
--- | --- | --- | ---
NOTSET | 0 | N/A | 未設定
DEBUG | 10 | logging.debug() | 除錯
INFO | 20 | logging.info() | 訊息
WARNING | 30 | logging.warning() | 警告
ERROR | 40 | logging.error() | 錯誤
CRITICAL | 50 | logging.critical() | 嚴重錯誤

- Python等級數值

```Python
import logging

print(logging.NOTSET)   # 0
print(logging.DEBUG)    # 10
print(logging.INFO)     # 20
print(logging.WARNING)  # 30
print(logging.ERROR)    # 40
print(logging.CRITICAL) # 50

print(logging.getLevelName(0))    # NOTSET
print(logging.getLevelName(10))   # DEBUG
print(logging.getLevelName(20))   # INFO
print(logging.getLevelName(30))   # WARNING
print(logging.getLevelName(40))   # ERROR
print(logging.getLevelName(50))   # CRITICAL
```

## 輸出Logging

Logging模組預設等級為WARNING

大於或等於 WARNING 等級的訊息才會被記錄

```Python
import logging

logging.debug('debug message')
logging.info('info message')
logging.warning('warning message')
logging.error('error message')
logging.critical('critical message')
```

輸出結果:

```Shell
WARNING:root:warning message
ERROR:root:error message
CRITICAL:root:critical message
```

- 調整輸出等級

設定輸出等級為DEBUG，所有等級的訊息皆會輸出

```Python
logging.basicConfig(level=logging.DEBUG)
```

- 堆疊追蹤

紀錄完整的堆疊追蹤 (stack traces)，在 logging.error() 加上 exc_info 參數，並將該參數設為 True，就可以紀錄 Exception；若沒有加上 exc_info=True 則無法紀錄 Exception

```Python
logging.error("Catch an exception.", exc_info=True)
```

在 logging 內紀錄 exception 訊息，可使用 logging.exception()，它會將 exception 添加至訊息中，此方法的等級為 ERROR，也就是說 logging.exception() 就等同於 logging.error(exc_info=True)

```Python
logging.exception('Catch an exception.')
```

## logging 輸出格式

預設的訊息輸出格式只有 levelname、name、message

格式化字串 | 說明
--- | ---
%(asctime)s | 日期時間, 格式為 YYYY-MM-DD HH:mm:SS,ms，例如：2021-07-19 21:20:30,123
%(filename)s | 模組檔名
%(funcName)s | 函數名稱
%(levelname)s | 日誌的等級名稱
%(levelno)s | 日誌的等級數值
%(lineno)d | 呼叫日誌函數所在的行數
%(message)s | 訊息
%(module)s | 模組名稱
%(name)s | logger 的名稱
%(pathname)s | 檔案的完整路徑 (如果可用)
%(process)d | process ID (如果可用)
%(thread)d | 執行緒 ID (如果可用)
%(threadName)s | 執行緒名稱

可將這些資訊加入 logging.basicConfig() 內的 format 參數

```Python
FORMAT = '%(asctime)s %(levelname)s: %(message)s'
logging.basicConfig(level=logging.DEBUG, format=FORMAT)
```

## 自訂輸出的時間格式

在 logging.basicConfig() 內的 datefmt 參數可設定所需的時間格式，要使用 time.strftime() 接受的時間格式

參數 | 說明
--- | ---
%Y | 長年份，例如：2019
%y | 短年份，例如：19
%m | 月份：01 ~ 12
%B | 月份完整名稱，例如：February
%b | 月份縮寫名稱，例如：Feb
%d | 日期：01 ~ 31
%H | 小時 (24 小時制)：00 ~ 23
%I | 小時 (12 小時制)：01 ~ 12
%w | 星期：0 ~ 6，0 代表星期日
%A | 星期完整名稱，例如：Friday
%a | 星期縮寫名稱，例如：Fri
%P | AM 或 PM
%M | 分鐘：00 ~ 59
%S | 秒：00 ~ 61

```Python
LOGGING_FORMAT = '%(asctime)s %(levelname)s: %(message)s'
DATE_FORMAT = '%Y%m%d %H:%M:%S'
logging.basicConfig(level=logging.DEBUG, format=LOGGING_FORMAT, datefmt=DATE_FORMAT)
```

## 儲存 logging

在 logging.basicConfig() 內的 filename 參數設定要儲存的日誌檔名，就可以將 logging 儲存

```Python
FORMAT = '%(asctime)s %(levelname)s: %(message)s'
logging.basicConfig(level=logging.DEBUG, filename='myLog.log', filemode='w', format=FORMAT)
```

預設 filemode 參數是設為 a，代表 append (附加) 的意思，每次執行程式時，Logging 會將新的訊息加在舊的訊息後面，不會覆蓋舊的訊息。若要改成新訊息覆蓋就訊息，那可以將 filemode 參數設為 w，代表 write 的意思

Reference:

<https://titangene.github.io/article/python-logging.html>

官方文件<https://docs.python.org/3/library/logging.html>