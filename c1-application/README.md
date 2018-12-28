# [打印申请表](http://139.59.240.22:8001/)

自用打印申请表

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
* Clone the repo: `$ git clone https://github.com/qukaile/c1-application.git`.
* `$ cd c1-application`.
* 安装 django : `$ pip install Django`.
* 安装 reportlab :`$ conda install reportlab`.
* 安装 PyPDF2 :`$ pip install PyPDF2`.
* 开启 8001 端口: `$ sudo iptables -I INPUT -p tcp -s 0.0.0.0/0 --dport 8001 -j ACCEPT`.
* 上线应用: `$ python manage.py runserver 0.0.0.0:8001`.
```

### More

放在云服务器里，可以编写简单的shell脚本：
```
$ vim c1-application.sh

#!/bin/bash
source my_python3/bin/activate
cd c1-application
python manage.py runserver 0.0.0.0:8001

$ chmod +x c1-application.sh
$ screen -S c1-application  # 创建一个名字为c1-application的会话
$ ./c1-application2.sh
快捷键Ctrl+a d(即按住Ctrl，依次再按a,d)
```

### 备忘

```
* `$ screen -ls` 列出当前存在的会话列表
* `$ screen -r c1-application` 恢复会话
* `$ exit` 关闭会话.
```

### 定时任务

```
$ vim gov122_dingshi

#!/bin/bash
cd /root/
source my_python3/bin/activate
cd /root/c1-print/c1-application/
python polls_c1_print/gov122_Requests.py


保存在 /etc/cron.hourly 文件夹内

$ chmod +x gov122_dingshi
$ ./gov122_dingshi

Ubuntu调用run-parts命令，定时运行四个目录下的所有脚本。
/etc/cron.hourly下的脚本会被每小时运行一次，在每小时的17分时运行。
/etc/cron.daily下的脚本会被每天运行一次，在每天6点25分运行。
/etc/cron.weekly下的脚本会被每周运行一次，在每周第7天的6点47分运行。
/etc/cron.monthly下的脚本会被每月运行一次，在每月1号的6点52分运行。
只需要把计划运行的脚本放到相应目录中就可以了。需要注意：
1.脚本文件的名称不能包含“.”符号。你可以写成“im-alarm”，但不要写成“im-alarm.sh”。（因为命名问题，遇到过不执行的情况）
2.sudo /etc/init.d/cron restart
```