---
layout: page
title: Bitnami and mySQL
description: Bitnami and mySQL.
---
*Updates: 4/5/2019*
Now I usually use KVM and docker.

**The post below is old and included here only for my documentation **

*Last updated: 9/7/2016*

#### Install
Usually the bitnami containers are installed under /opt/. For mysql, you will see the folder my sql in container for example the path below


> /opt/mysql/lampstack-5.4.13-1/mysql/

#### Start and stop container
Use the script at the root of container

```
./ctlscript.sh start
```

for status

```
./ctlscript.sh status
```

#### Logs
Logs are available at

> /opt/mysql/lampstack-5.4.13-1/mysql/data$ vi mysqld.log


#### Issues starting mysql
If you see the following on the command line (happened to me twice),

>Warning: World-writable config file '/opt/mysql/lampstack-5.4.13-1/mysql/my.cnf' is ignored
>Warning: World-writable config file '/opt/mysql/lampstack-5.4.13-1/mysql/my.cnf' is ignored
>161115 09:30:24 mysqld_safe Logging to >'/opt/mysql/lampstack-5.4.13-1/mysql/data/mysqld.log'.
>161115 09:30:24 mysqld_safe Starting mysqld daemon with databases from >/opt/mysql/lampstack-5.4.13-1/mysql/data
>161115 09:30:26 mysqld_safe mysqld from pid file >/opt/mysql/lampstack-5.4.13-1/mysql/data/mysqld.pid ende


and the log file will look like this


>155 InnoDB: Restoring possible half-written data pages from the doublewrite
>156 InnoDB: buffer...
>157 161115  9:30:24  InnoDB: Waiting for the background threads to start
>158 161115  9:30:25 InnoDB: 1.1.8 started; log sequence number 669048462
>159 161115  9:30:25 [ERROR] /opt/mysql/lampstack-5.4.13-1/mysql/bin/mysqld.bin: unknown >variable 'defaults-file=/opt/mys    ql/lampstack-5.4.13-1/mysql/my.cnf'
>160 161115  9:30:25 [ERROR] Aborting
>161
>162 161115  9:30:25  InnoDB: Starting shutdown...
>163 161115  9:30:26  InnoDB: Shutdown completed; log sequence number 669048462
>164 161115  9:30:26 [Note] /opt/mysql/lampstack-5.4.13-1/mysql/bin/mysqld.bin: Shutdown >complete
>165
>166 161115 09:30:26 mysqld_safe mysqld from pid file >/opt/mysql/lampstack-5.4.13-1/mysql/data/mysqld.pid ended



It means that the file /opt/mysql/lampstack5.4/mysql/bin/mysqld  has a line which is causing issues. See below


```
  1 #!/bin/sh
  2 LD_LIBRARY_PATH=/opt/mysql/lampstack-5.4.13-1/mysql/lib:$LD_LIBRARY_PATH
  3 export LD_LIBRARY_PATH
  4 case "$@" in
  5   *--no-defaults*)
  6     exec $0.bin "$@"
  7     exit
  8 esac
  9 exec $0.bin --defaults-file=/opt/mysql/lampstack-5.4.13-1/mysql/my.cnf "$@"


```

see the last line , just make it look like this


```
exec $0.bin "$@"
 13 #--defaults-file=/opt/redmine/redmine-2.6.1-0/mysql/my.cnf "$@"

```

Start stack again by using the following command

```
./ctl

```


#### phpmyadmin

In bitnami stack, phpmyadmin is at

/opt/mysql/lampstack-5.4.13-1/apps/phpmyadmin/

and its ini is at

/opt/mysql/lampstack-5.4.13-1/apps/phpmyadmin/htdocs/config.inc.php
