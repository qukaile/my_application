# [my_office_application](http://#/)

自用云主机 Django 应用程序

## Quick start

Several quick start options are available:

* 系统环境采用 Ubuntu 16.04 及LNMP配置 。ubuntu 配置及 Python3 环境搭建：
```
1. $ sudo apt-get update
2. # 检查 python版本 >= 3
3. $ pip install virtualenv
4. # 基于 python3.6 创建一个名为my_python3 的环境
$ virtualenv --no-site-packages --python=python3.6 my_python3
5. # 激活环境
* $ source my_python3/bin/activate
6. # Clone the repo
    * $ cd my_office_application
7. # 安装依赖环境
    * 安装 django : $ pip install Django
    * 安装 reportlab : $ pip install reportlab
    * 安装 Requests : $ pip install Requests
    * 安装 mysqlclient : $ pip install mysqlclient
    * 安装 PyPDF2 : $ pip install PyPDF2
        * PyPDF2如果安装失败，需要下载 PyPDF2-xxx.tar.gz （例PyPDF2-1.26.0.tar.gz）
        * 执行 $ pip install PyPDF2-xxx.tar.gz
8. # 其他
    * 数据库操作
        $ python manage.py makemigrations
        $ python manage.py migrate
        $ python manage.py createsuperuser
    * 执行测试 $ python manage.py test -v 2
9. # 部署
    server {
      listen 8081;
      server_name xx; # 本机IP
      charset utf-8;
      client_max_body_size 75M;
      location /static {
        alias /data/wwwroot/default/static; # Django静态文件目录在系统中的绝对路径
    }
      location / {
        uwsgi_pass xx:8001; # 本机IP
        include /usr/local/nginx/conf/uwsgi_params; # 确保路径中有此文件
        }
    }
    * 进入python3虚拟环境，执行 uwsgi --socket :8001 --module app.wsgi --chmod-socket=664 --daemonize /root/my_office_application/uwsgi.log
```

### What's included

Within the download you'll find the following directories and files, logically grouping common assets and providing both compiled and minified variations. You'll see something like this:

```
my_office_application/
├── app/
│   ├── settings.py # 新增 app 需要插入进 INSTALLED_APPS
│   └── urls.py # 新增 app 需要增加 url 路由
├── files/
│   ├── models.py # File, Fuhe, Kuaidi 三个模型
│   ├── views.py # FileCreate(), get_name() 两个视图函数
│   └── urls.py # 新建档案，批量查询 两个路由
├── gov122/
│   ├── gov122_Requests.py # 爬虫文件
│   ├── README.md # 爬虫文件的配置和使用
│   ├── models.py # Book(手出申请表用), Gov122YuYue 两个模型
│   ├── views.py # detail(), BookCreate(), lu_ru(), lu_ru_ming_dan(), 
│   │                gov122_jihua_gongbu(), pdf_view() 六个视图函数
│   └── urls.py # 对应视图函数：1)手出申请表add、detail和输出pdf;2)录入计算补考费-单页面;
│                               3)考试计划和公布-定时Requests爬虫,更新在gov122_data.json文件-单页面列出数据
├── kaipiao/
│   ├── models.py # File, Fuhe, Kuaidi 三个模型
│   ├── views.py # FileCreate(), get_name() 两个视图函数
│   └── urls.py # 新建档案，批量查询 两个路由
├── mix_part1/
│   ├── models.py # File, Fuhe, Kuaidi 三个模型
│   ├── views.py # FileCreate(), get_name() 两个视图函数
│   └── urls.py # 新建档案，批量查询 两个路由
├── mix_part2/
│   ├── models.py # File, Fuhe, Kuaidi 三个模型
│   ├── views.py # FileCreate(), get_name() 两个视图函数
│   └── urls.py # 新建档案，批量查询 两个路由
├── mix_part3/
│   ├── models.py # File, Fuhe, Kuaidi 三个模型
│   ├── views.py # FileCreate(), get_name() 两个视图函数
│   └── urls.py # 新建档案，批量查询 两个路由
├── shouli/
│   ├── models.py # File, Fuhe, Kuaidi 三个模型
│   ├── views.py # FileCreate(), get_name() 两个视图函数
│   └── urls.py # 新建档案，批量查询 两个路由
├── todo/
│   ├── models.py # File, Fuhe, Kuaidi 三个模型
│   ├── views.py # FileCreate(), get_name() 两个视图函数
│   └── urls.py # 新建档案，批量查询 两个路由
└── scrapy.cfg
```

### 备忘

```
* 之后每次修改 settings.py 或其他后执行
netstat -antup  // 查看 uwsgi 进程号，一般都为3922/18233
kill -HUP 18233 // 杀死该进程，即重启了 Django 网站
进入python3虚拟环境，进入 my_office_application 目录
执行 
uwsgi --socket :8001 --module app.wsgi --chmod-socket=664 --daemonize /root/my_office_application/uwsgi.log

常用命令：
    python manage.py makemigrations
    python manage.py migrate

    python manage.py runserver 0:8000

    python manage.py startapp xx
    python manage.py test -v 2
    python manage.py shell
    python manage.py createsuperuser
```
 
### 异常处理

* 创建未自动创建的表,有些情况下会出现数据库表未自动创建的问题
```
* 运行 python manage.py makemigrations students
* 运行 python manage.py migrate

* lnmp安装后mysql会启动不了The server quit without updating PID file
拷贝`/etc/my.conf`替换到`/etc/mysql/my.conf`

* 数据库保存时间比预期提前8小时的问题
`USE_TZ = False` 配置注释掉此项。USE_TZ默认: False；这是一个布尔值,用来指定是否使用指定的时区(TIME_ZONE)的时间.若为 True, 则Django 会使用内建的时区的时间;否则, Django 将会使用本地的时间。

* 已知问题files_file数据表id_card字段长度如果不为18会报错
暂时解决办法： `SELECT * FROM `files_file数据表` WHERE LENGTH(id_card) != 18`
将查询到的数据增补到18位

* mysql的字符串修改为utf8
    * 进入mysql(mysql -uroot -p),查看当前数据库字符集(status;)
    * vim /etc/mysql/my.cnf
        * [client]
        * default-character-set=utf8
        * [mysqld]
        * default-storage-engine=INNODB
        * character-set-server=utf8
        * collation-server=utf8_general_ci
    * 重启mysql(/etc/init.d/mysql stop   /etc/init.d/mysql  start)
    * 进入mysql查看字符集 show variables like "%character%";show variables like "%collation%";
    * 创建数据库的时候：CREATE DATABASE `youyidb` CHARACTER SET 'utf8' COLLATE 'utf8_general_ci';
```