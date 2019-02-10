# [my_tools](#)

我的命令列(command line)的程式。


## Table of contents

* [Quick start](#quick-start)


## Quick start

Several quick start options are available:

* 系统环境采用 Ubuntu 16.04 及LNMP配置 。ubuntu 配置及 Python3 环境搭建：
```
1. $ sudo apt-get update
2. # 检查 python版本 >= 3
3. $ pip install virtualenv
4. # 基于 python3.7 创建一个名为my_python3 的环境
$ virtualenv --no-site-packages --python=python3.7 my_python3
5. # 激活环境
* $ source my_python3/bin/activate
6. # Clone the repo
    * $ cd my_tools
7. # 安装依赖环境
    * $ pip install -r requirements.txt
```

* 1、check_on_Friday 每周五查看名额是否公布
`python app/check_on_Friday.py`

* 2、spider_job.py 自动爬取最新活动，有更新就邮件提醒
```
$ screen -S my_daily  # 创建一个名字为 my_daily 的会话
$ source /root/my_python3/bin/activate
$ python setup.py
* 快捷键Ctrl+a d(即按住Ctrl，依次再按a,d)

备忘:
$ screen -ls 列出当前存在的会话列表
$ screen -r my_daily 恢复会话
$ exit 关闭会话.
```

* 3、selenium-2-py.py 自用自动上传xls文件内容到服务器
```
1. 此脚本需要配合 chrone 的 selenium 拓展程序，
2. 录制或编写一段selenium脚本，批量下载学员考试、预约信息xls文件。
3. 复制 selenium-2-py.py 到 chrome 下载目录
$ python selenium-2-py.py
4. 上传内容，完毕后删除xls文件
```

* 4、youchu.py 邮储银行模拟操作查看抢购商品库存
```
1. 打开雷电模拟器，进入邮储银行，且已扫码，进入库存页面 商品库存0件
2. 详情参见 py 文件
```

* 5、download_ts.py 爬取m3u8地址的所有ts文件，下载，合并
```
1. 修改 begin_url , url 参数
$ python download_ts.py
# 爬取m3u8地址的所有ts文件到 C:/Users/kl/Desktop/video.txt
# IDM 导入 video.txt 下载
# cmd 进入ts文件下载目录，执行 copy/b  *.ts  new.ts
```

