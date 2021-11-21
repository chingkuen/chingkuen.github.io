---
layout: post
title: Python with Json
subtitle: Python with Json
categories: python
tags: [python]
---
# Python Json

## data.json

```Json
{ "employee_id":"21000785","birth_date":"1026","parking_date":["2021-12-03", "2021-12-07","2021-12-10"]}
```

## 讀取json

- 讀取json檔案

使用Python內建json模組的load()

```Python
import json

with open("data.json") as f:
    parking_data = json.load(f)

    print ("employee_id is " + parking_data["employee_id"])
    print ("birth_date is" + parking_data["birth_date"])
    print ("parking_date is", parking_data["parking_date"])
```

- 讀取python中的json字串

使用json模組的loads(), 轉換Python的string為dict

```Python
json_data_from_sting = '{ "employee_id":"21000785","birth_date":"1026","parking_date":["2021-12-03", "2021-12-07","2021-12-10"]}'
parking_data_from_string = json.loads(json_data_from_sting)
print (type(parking_data_from_string),parking_data_from_string)
```

- 讀取python中的dict

使用json模組的dumps(), 轉換Python的dict為string

```Python
jason_data_from_dict = { "employee_id":"21000785","birth_date":"1026","parking_date":["2021-12-03", "2021-12-07","2021-12-10"]}
parking_data_from_dict = json.dumps(jason_data_from_dict, indent=4)
print (type(parking_data_from_dict), parking_data_from_dict)
```

## 寫入json

使用json模組的dump(), 儲存Python的dict為json檔案

```Python
with open("output.json", "w") as write_json:
    json.dump(parking_data_from_string, write_json, indent = 4)
```
