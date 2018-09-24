# Django　Blog

基于`python3.7.0`和`Django2.1.1`的个人博客。   

## 主要功能：
- 文章，页面，分类目录，标签。文章详情页面支持上下篇文章快速跳转，支持`Markdown`语法，支持代码高亮
- 支持回到页面顶部
- 支持评论功能。
- 增加侧边栏，日期归档，最新文章，最多阅读，标签汇总等。
- 支持在文章中插入图片链接并显示图片
- 支持对全部文章进行关键字搜索

## 所需依赖
使用pip安装：  

`pip install mysqlclient`

`pip install markdown`

`pip install Pygments`

### 配置数据库
配置都是在`setting.py`中.部分配置迁移到了后台配置中。

 修改`DjangoBlog/setting.py` 修改数据库配置，如下所示(例子中使用的是mysql,使用其它数据库请参考django官方文档)：
 
     DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': 'my_blog',
            'USER': 'root',
            'PASSWORD': 'password',
            'HOST': 'host',
            'PORT': 3306,
        }
    }

### 创建数据库

mysql数据库中执行:
```sql
CREATE DATABASE `my_blog`;
```
 终端下执行:

    ./manage.py makemigrations
    ./manage.py migrate
### 创建超级用户

 终端下执行:

    ./manage.py createsuperuser
### 创建测试数据
终端下执行:

    ./manage.py create_testdata
### 收集静态文件
终端下执行:  

    ./manage.py collectstatic --noinput
    ./manage.py compress --force
### 开始运行：
 执行：
 `./manage.py runserver 127.0.0.1:8000`


 浏览器打开: http://127.0.0.1:8000/  就可以看到效果了。

 ## 问题相关
 
 markdown 语法: https://www.appinn.com/markdown/

