# Django

#### 1.创建项目

	- 命令行
		
		```
		django-admin startproject 项目名称
		```


​		

#### 2.启动项目

 - 命令行

     ```
     py python manage.py runserve
     ```

     

#### 3.form表单注意的点

​	1.form标签的属性action指定提交的地址(不写默认当前地址),method请求方式(默认get)
​	2.input标签要有name属性.有的标签还需要value
​	3.有一个button按钮或者是type='submit'的input



#### 4.目前要提交post请求的必要操作：

##### 	在settings py 中注释一个中间件：

```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```



#### 5.重定向

##### 	request:

​		request.method 请求方式GET POST

​		request.POST form表单提交post请求的数据

​		request.GET URL上窗体参数（查询参数）

##### 	登录成功跳转到别的页面(redirect)

```python
from django.shortcuts import render, HttpResponse, redirect

# 跳转到别的页面
redirect('http://www.baidu.com')
```



#### 6.APP

##### 创建APP:

###### 	1.命令行(在terminal执行)

​		python manage.py startapp app名称

###### 	2.通过 run manage.py task

​		tools -> run manage.py task -> 出现窗口 输入命令即可

##### 注册APP:

```python
INSTALLED_APPS = [
    'django.contrib.staticfiles',
    # 'app01'  # 直接写app名称
    'app01.apps.App01Config' # 推荐写法
]
```





#### 7.ORM

##### 对应关系:

类 --> 表

对象 --> 数据行(记录)

属性 --> 字段



##### 使用ORM:

1.在settings中配置数据库的连接

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

2.在app下的models.py中写类：

```python
class User(models.Model):
    username = models.CharField(max_length=32)  # varchar(32)
    password = models.CharField(max_length=32)
```

3.执行数据库迁移的命令

```python
python manage.py makemigrations	# 检测所有app下载的models.py文件有什么变化
python manage.py migrate	# 数据库的迁移 将变更的记录同步到数据库中
```

