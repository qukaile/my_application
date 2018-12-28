# [my_django_all_in_one](http://#/)

自用 Django 应用程序

## Quick start

Several quick start options are available:

* 系统环境采用 Ubuntu 16.04 及LNMP配置 。ubuntu 配置及 Python3 环境搭建：
```
1. $ sudo apt-get update
2. # 检查 python版本 >= 3
3. $ pip install virtualenv
4. # 基于 python3.7 创建一个名为my_python3 的环境
* $ virtualenv --no-site-packages --python=python3.7 my_python3
5. # 激活环境
* $ source my_python3/bin/activate
6. # Clone the repo
7. # 安装依赖环境
* 安装 django : $ pip install Django
8. # 其他
    * 数据库操作
        $ python manage.py makemigrations
        $ python manage.py migrate
        $ python manage.py createsuperuser
9. 开启 8002 端口: $ sudo iptables -I INPUT -p tcp -s 0.0.0.0/0 --dport 8002 -j ACCEPT
```

### More

放在云服务器里，可以编写简单的shell脚本：
```
$ vim my_django_all_in_one.sh

#!/bin/bash
source /root/my_python3/bin/activate
cd my_django_all_in_one
python manage.py runserver 0.0.0.0:8002

$ chmod +x my_django_all_in_one.sh
$ screen -S my_django_all_in_one  # 创建一个名字为 my_django_all_in_one 的会话
$ ./my_django_all_in_one.sh
快捷键Ctrl+a d(即按住Ctrl，依次再按a,d) 

* `$ screen -ls` 列出当前存在的会话列表
* `$ screen -r my_django_all_in_one` 恢复会话
* `$ exit` 关闭会话.

常用命令：
    python manage.py startapp xx
    python manage.py test -v 2
    python manage.py shell
```


# [艾宾浩斯记忆法应用程序 forgetting_curve ](http://#/)

自用艾宾浩斯记忆法应用程序

## 艾宾浩斯记忆法应用程序 Quick start

Several quick start options are available:
```
* 执行测试 $ python manage.py test -v 2
```

# [以撒的结合app](http://#/)

自用以撒的结合app, 可以查找、列出名称、充能、描述...，在admin界面修改描述。

## 以撒的结合app Quick start

Several quick start options are available:

```
1. # 安装依赖环境
    * 安装 requests : $ pip install django-model-utils
```


# [一注基础考试复习题集](http://#/)

边动手更新题库，边做题巩固。本习题集适合参加一级注册结构工程师执业资格考试基础考试的考生复习备考使用；
同时做题查看以撒的结合。
以撒的部分资源来自于：http://isaac.icecat.cc/


# [zhuan-ke-application](http://#/)

zhuan-ke-application 应用程序

## ZK Quick start

```
1. # 安装依赖环境
    * 安装 requests : $ pip install Requests
    * 安装 beautifulsoup : $ pip install beautifulsoup4
    * 安装 schedule : $ pip install schedule
```

### ZK More
  
```
$ screen -S web_spider_zhuan_ke  # 创建一个名字为 web_spider_zhuan_ke 的会话，以便查看定时爬虫
$ source /root/my_python3/bin/activate
$ cd /root/my_django_all_in_one/zhuan_ke
$ python web_spider.py
快捷键Ctrl+a d(即按住Ctrl，依次再按a,d)

* `$ screen -ls` 列出当前存在的会话列表
* `$ screen -r web_spider_zhuan_ke` 恢复会话
* `$ exit` 关闭会话.
```

### ZK 备忘

```
清理
source /root/my_python3/bin/activate
cd /root/my_django_all_in_one
python manage.py shell

from zhuan_ke.models import Todo
Todo.objects.filter(finished=1).delete()

增删爬虫关键字
cd /root/my_django_all_in_one/zhuan_ke
vim exclude_list.py
```


# What's included

Within the download you'll find the following directories and files, logically grouping common assets and providing both compiled and minified variations. You'll see something like this:

```
my_django_all_in_one/
├── app/
│   ├── __init__.py
│   ├── forms.py
│   ├── settings.py
│   ├── urls.py
│   ├── views.py
│   ├── wsgi.py
│   └── __pyache__/
│        └── ...
├── templates/
│   ├── base_site.html
│   ├── home.html
│   └── login.html
├── forgetting_curve/
│   └── ...
├── yi_sa/
│   └── ...
├── yi_zhu/
│   └── ...
├── zhuan_ke/
│   └── ...
├── manage.py
├── db.sqlite3
└── README.md
```