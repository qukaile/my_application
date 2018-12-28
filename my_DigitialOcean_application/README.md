# [my_DigitialOcean_application](http://#/)

自用 Digitial Ocean 云主机 Django 应用程序

## Quick start

Several quick start options are available:

* 系统环境采用 Ubuntu 16.04 。ubuntu 配置及 Python3 环境搭建：
```
1. $ sudo apt-get update
2. # 清华镜像站下载最新 Miniconda3-latest-Linux-x86_64.sh
$ https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/ 
$ bash Miniconda3-latest-Linux-x86_64.sh
3. # 基于 python3.6 创建一个名为test_py3 的环境
$ conda create --name my_python3 python=3.6
4. $ source activate my_python3
* Clone the repo: `$ git clone https://github.com/qukaile/my_DigitialOcean_application.git`.
* `$ cd my_DigitialOcean_application`.
* 安装 django : `$ pip install Django`.
* 安装 reportlab :`$ conda install reportlab`.
* 安装 PyPDF2 :`$ pip install PyPDF2`.
* `$ apt-get install mysql-server`.(可选)
* `$ conda install -c bioconda mysqlclient`.
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

### 备忘

```
* 开启 8001 端口: `$ sudo iptables -I INPUT -p tcp -s 0.0.0.0/0 --dport 8001 -j ACCEPT`.
source activate my_python3
cd <dir>
uwsgi --ini hello_uwsgi.ini
之后每次修改 settings.py 或其他后执行
netstat -antup  // 查看 uwsgi 进程号，一般都为3922/18233
kill -HUP 18233 // 杀死该进程，即重启了 Django 网站
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
```