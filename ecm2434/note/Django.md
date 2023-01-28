## django
### create a django project using command line
```
django-admin startproject <projectName>
```

i.e.
```
django-admin startproject mysite
```

- file structure
```shell
mysite/
├── manage.p		#  manage project(start project, create app, manage data(don't change)
└── mysite
    ├── asgi.py		# respond netwoek request(don't change)
    ├── __init__.py
    ├── settings.py	# configurate project(template, db, register app) (manipulate)
    ├── urls.py		# url & function (manipulate)
    └── wsgi.py		# respond network request(don't change)
```

### app
- what 
A project may contain several apps to deal with different functionalities(user management, backend management, website, api

- create
```shell
<target django dir path>python3 manage.py startapp <appname>
```

i.e.
```
(base) kristin@kristin-PC:~/study/fun/preECM2434/self/mysite$ python3 manage.py startapp app01
```

```
(base) kristin@kristin-PC:~/study/fun/preECM2434/self/mysite$ ls
app01  manage.py  mysite
```

```
├── app01
│   ├── __init__.py
│   ├── admin.py         【固定，不用动】django默认提供了admin后台管理。
│   ├── apps.py          【固定，不用动】app启动类
│   ├── migrations       【固定，不用动】数据库变更记录
│   │   └── __init__.py
│   ├── models.py        【**重要**】，对数据库操作。
│   ├── tests.py         【固定，不用动】单元测试
│   └── views.py         【**重要**】，函数。
├── manage.py
└── mysite2
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py          【URL->函数】
    └── wsgi.py
```

```
..
├── mysite
│   ├── app01
│   │   ├── admin.py
│   │   ├── apps.py
│   │   ├── __init__.py
│   │   ├── migrations
│   │   │   └── __init__.py
│   │   ├── models.py
│   │   ├── tests.py
│   │   └── views.py
│   ├── manage.py
│   └── mysite
│       ├── asgi.py
│       ├── __init__.py
│       ├── settings.py
│       ├── urls.py
│       └── wsgi.py
```

### run
- register app [apps.py] [settings.py]

- url and appName.views 的对应关系 [urls.py] 

- edit views.py

- run Django project

Inside the Django dir  
```
python3 manage.py runserver
```

```
(base) kristin@kristin-PC:~/study/fun/preECM2434/self/mysite$ python3 manage.py  runserver
```

### static files
- static dir layout

### template language
```python
def tpl(request):
    name = "poker"
    role_list = ['waiter', 'cook', 'manager']
    user_info = {"name":"alex", "age":24, "gender": "male"}
    user_info_list = [
        {"name":"alex", "age":24, "gender": "male"},
        {"name":"james", "age":23, "gender": "male"},
        {"name":"liv", "age":22, "gender": "female"},
    ]
    return render(request, "tpl.html", {"name":name, "roles_list":role_list, "user_info":user_info, "user_info_list":user_info_list})
```

```html
<h1>templates syntax</h1>
<h2>Single arg</h2>
<li>Name: {{ name }}</li>

<h2>List</h2>
<li>Roles: {{ roles_list }}</li>
<li>Role1: {{ roles_list.0 }}</li>
<li>Role1: {{ roles_list.1 }}</li>
<li>Role1: {{ roles_list.2 }}</li>

<h2>List Loop</h2>
<div>
    {% for item in roles_list %}
        <span>{{ item }}</span>
    {% endfor %}
</div>

<h2>Dic</h2>
<div>
    {{ user_info }}<br>
    {{ user_info.name }}<br>
    {{ user_info.age}}<br>
    {{ user_info.gender }}<br>
</div>

<h2>Dic loop</h2>
<h3>get keys</h3>
<div>
    {% for k in user_info.keys %}
        <li>{{ k }}</li>
    {% endfor %}
</div>

<h3>get values</h3>
<div>
    {% for v in user_info.values %}
    <li>{{ v }}</li>
    {% endfor %}
</div>

<h3>get items and values</h3>
<div>
    {% for k, v in user_info.items %}
    <li>{{ k }} = {{ v }}</li>
    {% endfor %}
</div>

<h2>list of dics</h2>
<div>
    {% for item in user_info_list %}
    <div>{{ item.name }} {{ item.age }} {{ item.gender }}</div>
    {% endfor %}
</div>

<h2>condition</h2>
{% if name == "poker" %}
    <h4>My name is poker</h4>
{% elif name == "toker" %}
    <h4>My name is toker</h4>
{% else %}
    <h4>I don't have any name :(</h4>
{% endif %}
```

### Login Example

### ORM
- sqlite  
	- cheat sheet  
https://d17h27t6h515a5.cloudfront.net/topher/2016/September/57ed880e_sql-sqlite-commands-cheat-sheet/sql-sqlite-commands-cheat-sheet.pdf  

	- toturtial
https://sqlite.org/cli.html#getting_started

1. Create a new db
- setting.py  
https://docs.djangoproject.com/en/4.1/ref/settings/#databases  

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': 'mydatabase',
    }
}
```

- app01/model.py

```python
from django.db import models

# Create your models here.
class UserInfo(models.Model):
    name = models.CharField(max_length=20)
    password = models.CharField(max_length=20)
    age = models.IntegerField()

"""
create table UserInfo(
    id bigint auto_increment primary key,
    name varchar(20),
    password varchar(20),
    age int
)
"""
```

Run following commands in project's root directory in the shell  
If don't want a table anymore, comment the class, and run these command gagin.  
App needs to be registered in advance.  

```shell
python3 manage.py makemigrations
python3 manage.py migrate
```

Using sqlite shell  
```shell
python3 manage.py dbshell
```

2. Add a new colum 
When adding a new column in a table, since there may already be data in the existing column, the new column must specify the data corresponding to the new column:

- Enter a value manually
```shell
(base) kristin@kristin-PC:~/study/fun/preECM2434/self/mysite$ python3 manage.py makemigrations
It is impossible to add a non-nullable field 'size' to userinfo without specifying a default. This is because the database needs something to populate existing rows.
Please select a fix:
 1) Provide a one-off default now (will be set on all existing rows with a null value for this column)
 2) Quit and manually define a default value in models.py.
Select an option: 1
Please enter the default value as valid Python.
The datetime and django.utils.timezone modules are available, so it is possible to provide e.g. timezone.now as a value.
Type 'exit' to exit this prompt
>>> 1
Migrations for 'app01':
  app01/migrations/0002_userinfo_size.py
    - Add field size to userinfo
(base) kristin@kristin-PC:~/study/fun/preECM2434/self/mysite$ python3 manage.py dbshell
```

- Set default value

```python
age = models.IntegerField(default=2)
```

- Allow to be null
```python
data = models.IntegerField(null=True, blank=True)
```

3. Django action table data

- add data

```python
UserInfo.objects.create(name="poker", password="123", age=25, size=1)
```

```shell
sqlite> select * from app01_userinfo; 
1|poker|123|1||25
```

- delete data

```python
# delete data
UserInfo.objects.filter(id=2).delete()

# delete all the data in the table
UserInfo.objects.all().delete()
```

- get data

```python
data_list = UserInfo.objects.all()
print(data_list)
for obj in data_list:
    print(obj.id, obj.name, obj.password, obj.age)
```

- update data
```python
UserInfo.objects.filter(name="roker").update(age=35)
```

## Reference
https://docs.djangoproject.com/en/4.0/intro/tutorial01/  

https://blog.csdn.net/qq_43139145/category_12125712.html  
