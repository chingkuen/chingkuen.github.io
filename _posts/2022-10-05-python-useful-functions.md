---
layout: post
title: Python Useful Function
subtitle: Python Useful Function
categories: python
tags: [python]
---

## Python useful function

### map

map(function, iterable)

```python
def square(x):
    return x**2
print(map(square, [1,2,3,4,5]))
print(list(map(square, [1,2,3,4,5])))
```

Result:

```python
<map object at 0x7fdad7858100>
[1, 4, 9, 16, 25]
```

## lambda

lambda arguments: expressions:

```python
nums1 = [1,2,3,4,5]
nums2 = []

for i in nums1:
    x = lambda i : i**2
    nums2.append(x(i))
print(nums2)
```

Result:

```python
[1, 4, 9, 16, 25]
```

## Index Sort

```python
students = [
['Joey', 'A', 15],
['Monica', 'B', 10],
['Ross', 'C', 8],
['Rachel', 'B', 12]
]
student_sort_1 = sorted(students)
student_sort = sorted(students, key = lambda student : student[2])

print(student_sort_1)
print(student_sort)
```

Result:

```python3
[['Joey', 'A', 15], ['Monica', 'B', 10], ['Rachel', 'B', 12], ['Ross', 'C', 8]]
[['Ross', 'C', 8], ['Monica', 'B', 10], ['Rachel', 'B', 12], ['Joey', 'A', 15]]
```
