# Django　Blog

基于`python3.7.0`和`Django2.1.1`的个人博客。   文章，页面，分类目录，标签的添加，删除，编辑等。文章及页面支持`Markdown`，支持代码高亮。

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

 修改`DjangoBlog/setting.py` 修改数据库配置，如下所示：
 
     DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': 'djangoblog',
            'USER': 'root',
            'PASSWORD': 'password',
            'HOST': 'host',
            'PORT': 3306,
        }
    }

### 创建数据库

mysql数据库中执行:
```sql
CREATE DATABASE `djangoblog` /*!40100 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci */;
```
 然后终端下执行:

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
 `./manage.py runserver`





 浏览器打开: http://127.0.0.1:8000/  就可以看到效果了。
## 更多配置:
[更多配置介绍](/bin/config.md)
 ## 问题相关

 有任何问题欢迎提Issue,或者将问题描述发送至我邮箱 `liangliangyy#gmail.com`.我会尽快解答.推荐提交Issue方式.
