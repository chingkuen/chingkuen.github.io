---
layout: post
title: Python Flask
subtitle: Python Flask
categories: python
tags: [python][flask]
---
# Python Flask

```Python
    from flask import Flask

    app = Flask(__name__)

    def recent_2weeks():
    current_date = datetime.datetime.today()
    day_number = 1
    future_2weeks=[]
    while day_number <= 14:
        future_date = (current_date + datetime.timedelta(day_number))                    
        if future_date.strftime('%w') != "6" and future_date.strftime('%w') != "0":
            future_2weeks.append(future_date.strftime('%Y-%m-%d @ %w'))
        day_number += 1
    print (type(future_2weeks), future_2weeks)
    del future_date
    del day_number
    return future_2weeks
    
    @app.route('/',methods=['POST','GET'])
    def index():
        future_2weeks = []
        if request.method =='POST':
            date_list = ""
            employee_id = request.form.get('employee_id')
            birth_date = request.form.get('birth_date')
            target_date = request.form.getlist('date')
            if request.values['send']=='送出':
                return render_template('index.html', employee_id=employee_id, birth_date=birth_date, target_date=target_date, date_list=date_list)
        else:
            print ('Receive GET')
            future_2weeks = recent_2weeks()
            print(future_2weeks)
            return render_template('index.html', date_list=future_2weeks)
    
    @app.route('/second')
    def test():
        return redirect(url_for('index'))

    if __name__ == "__main__":
        app.run(host='0.0.0.0',port='5000', debug=True)
 ```

依照輸入改變的URL  

```Python
    @app.route("/")
    @app.route("/<name>")
    def test(name=None):
        if name==None:
            return "Hello World!"
        return "Hello "+name+"!"
```

## render_template()

> from flask import render_template  
or  
> from flask import Flask,render_template  

在這專案的資料夾內新增一個叫做templates的資料夾(記得是跟python檔案同層), Flask會到那邊尋找他所需要的html  

```Python
@app.route('/')
def index():
    return render_template('index.html')

@app.route('/second')
def test():
    return redirect(url_for('index'))
```

## url_for()

找到function名稱為index的把對方所指向的路由顯示出來  

## redirect()

重新導向連結  

## HTTP Methods

1. GET
2. HEAD
3. POST
4. PUT
5. DELETE
6. CONNECT
7. OPTIONS
8. TRACE
9. PATCH

## request

from flask import request

```Python
from flask import Flask,render_template,request

app=Flask(__name__)
@app.route('/',methods=['POST','GET'])
def index():
    if request.method =='POST':
        if request.values['send']=='送出':
            return render_template('index.html',employee_id=request.values['employee_id'],birth_date=request.values['birth_date'])
    return render_template('index.html',name="")

if __name__ == '__main__':
    app.run(host='0.0.0.0',port='5000',debug=True)
```

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Title</title>
</head>
<body>
    {% if date_list != "" %}
    <form method="post">
        <p>Please input employee ID</p>
        <input type="text" name="employee_id"><br>
        <p>Please input birth date</p>
        <input type="text" name="birth_date"><br><br>
        {% for day in date_list %}
        <p><label><input type="checkbox" name="date" value={{day}}>{{day}}</label></p>
        {% endfor %}
        <input type="submit" name="send" value="送出">
    </form>
    {% else %}
    <p>employee id is {{employee_id}}</p><br>
    <p>birth date is {{birth_date}}</p><br>
    <ul>
    {% for day in target_date %}
    <li>{{day}}</li>
    {% endfor %}
    </ul>
    {% endif %}
</body>
</html>
```

Flask:  
> @app.route('/',methods=['POST','GET'])  
> ‘/’允許的method有什麼

HTML部分:
> {% %} 程式碼外面要包這個  
> {{ }} variable顯現外面要加兩個大括號
> if 一定要 endif

---

Reference: <https://ithelp.ithome.com.tw/users/20120116/ironman/2532>