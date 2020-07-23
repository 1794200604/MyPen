#### 使用MYSQL数据库的流程：

##### 1.创建一个mysql数据库

##### 2.配置settings:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'login',
        'HOST': '127.0.0.1',
        'PORT': '3306',
        'USER': 'XiaoYu',
        'PASSWORD': '1535284697',
    }
}
```

##### 3.使用pymysql模块连接mysql数据库

##### 4.习惯写入与项目同名的文件夹下的__init__.py里

```python
import pymysql
pymysql.version_info = (1, 3, 13, "final", 0)
pymysql.install_as_MySQLdb()
```

##### 5.在app下的models里写入model

```python
class User(models.Model):
    username = models.CharField(max_length=32)  # varchar(32)
    password = models.CharField(max_length=32)
```

##### 6.执行数据库迁移的命令

```
python manage.py makemigrations
python manage.py migrate
```

