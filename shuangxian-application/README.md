# [shuangxian-application](http://#/)

自用 Django 应用程序

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
    * $ cd shuangxian-application
7. # 安装依赖环境
    * 安装 django : $ pip install Django
    * 安装 reportlab : $ pip install reportlab
8. # 其他
    * 数据库操作
        $ python manage.py makemigrations
        $ python manage.py migrate
        $ python manage.py createsuperuser
```

### More

放在云服务器里，可以编写简单的shell脚本：
```
$ vim c1-application.sh

#!/bin/bash
source my_python3/bin/activate
cd c1-application
python manage.py runserver 0.0.0.0:8001

$ chmod +x shuangxian.sh
$ screen -S shuangxian  # 创建一个名字为c1-application的会话
$ ./shuangxian.sh
快捷键Ctrl+a d(即按住Ctrl，依次再按a,d)

* `$ screen -ls` 列出当前存在的会话列表
* `$ screen -r shuangxian` 恢复会话
* `$ exit` 关闭会话.
```

### 备忘

```
* 内容 字段的json格式：
{"dan_jia3": "", "he_ji_jin_e": "", "dan_jia4": "", "jing_zhong3": "", "mao_zhong1": "", "dan_jia1": "", "jing_zhong2": "", "mao_zhong3": "", "jin_e2": "", "pi_zhong3": "", "pi_zhong4": "", "jing_zhong1": "", "jing_zhong4": "", "jin_e4": "", "pi_zhong2": "", "jin_e1": "", "mao_zhong2": "", "pi_zhong1": "", "dan_jia2": "", "jin_e3": "", "mao_zhong4": ""}
```