---
layout: post
title:  "pyhton3安装mysqlclient"
date:	2017-11-28  15：29
tags:
  - MySQL
---

##ubuntu pip 安装 mysqlclient 报错解决方法

要步入python3的开发环境了于是就上服务器用pyvenv搭建好了一套3.6的虚拟环境接着安装mysqlclient的时候出现了下面的错误
```
Collecting mysqlclient
  Using cached mysqlclient-1.3.12.tar.gz
    Complete output from command python setup.py egg_info:
    /bin/sh: 1: mysql_config: not found
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
      File "/tmp/pip-build-_yvru80n/mysqlclient/setup.py", line 17, in <module>
        metadata, options = get_config()
      File "/tmp/pip-build-_yvru80n/mysqlclient/setup_posix.py", line 44, in get_config
        libs = mysql_config("libs_r")
      File "/tmp/pip-build-_yvru80n/mysqlclient/setup_posix.py", line 26, in mysql_config
        raise EnvironmentError("%s not found" % (mysql_config.path,))
    OSError: mysql_config not found

    ----------------------------------------
Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-build-_yvru80n/mysqlclient/
```

后来查到了[GitHub的页面](https://github.com/PyMySQL/mysqlclient-python)发现是有缺失的包没装上，装上就好了

**Prerequisites**

You may need to install the Python and MySQL development headers and libraries like so:

sudo apt-get install python-dev libmysqlclient-dev # Debian / Ubuntu

sudo yum install python-devel mysql-devel # Red Hat / CentOS

On Windows, there are binary wheel you can install without MySQLConnector/C or MSVC.

**Note on Python 3 : if you are using python3 then you need to install python3-dev using the following command :**

sudo apt-get install python3-dev # debian / Ubuntu

sudo yum install python3-devel # Red Hat / CentOS

brew install mysql-connector-c # macOS (Homebrew)

