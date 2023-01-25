https://docs.djangoproject.com/en/4.0/intro/tutorial01/
## run flask as a server

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
