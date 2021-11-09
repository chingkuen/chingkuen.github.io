---
layout: post
title: Python Class
subtitle: Python Class
categories: python
tags: [python]
---
# Python Class

## Class

```python
class 類別名稱:
    類別變數

    def __init__(self):
        self.實體變數
    
    def 方法名稱(self):
        self.實體變數
```

- 類別變數, 也稱靜態變數, 用"類別.變數名稱"讀取
  
- 實體變數, 前面需加self.  

## 屬性與方法的存取權限

類別裡的變數(**屬性**)和函式(**方法**)

- 沒有底線: Public, 類別外部程式可存取

- 一個底線: Protected, 僅供類別內部或擴充此類別的程式存取

- 兩個底線: Private, 僅限類別內部程式存取

## shop.py

```Python
class Order():
    total = 0
    price = 35

    def __init__(self, amount=1, spicy=False):
        self.amount = amount
        self.spicy = spicy
        Order.total += amount
    
    def check(self):
        sum = Order.price * self.amount
        sauce = '加醬' if self.spicy else '不加醬'
        print(f'{self.amount}個肉圓{sauce}，共{sum}元。')
```

```Python
from shop import Order
order1 = Order(3, True)
order2 = Order(2)
order1.check()
Order.total


Order.price = 10
order1.check()
```

## @property裝飾器

- 在函式前面冠上"@property"裝飾器, 此函式被看待成**屬性**

```Python
@property
def number(self):
    return self._number

@property
def amount(self):
    return self._amount
```

## 把函式設成"可寫入的屬性"

```Python
@amount.settler
def amount(self, n):
    Order.total -= self._amount
    Order.total += n
    self._amount = n
```

## 靜態方法

- @staticmethod 靜態方法, 建立在類別上執行的方法

- **類別方法不用加self參數, 因self代表物件而非類別**

```Python
@staticmethod
    def quote():
        print(f'肉圓一個{Order.__price}元,加不加醬講清楚!')
```

- **_類別__屬性名稱**依舊可以改變

## 類別物件字串輸出功能

- __str__: 使用print()函式輸出物件，這個方法將被執行

- __repr__: 傳回以字串格式描述的物件資料

```Python
def __str__(self):
    sauce = '加醬' if self._spicy else '不加醬
    return f'{self._amount}個肉圓{sauce}

def __repr__(self):
    return f'{self.__class}, amount: {self._amount}, spicy: {self._spicy}
```
