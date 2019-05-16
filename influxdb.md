## 설치 ##

```
$ wget --no-check-certificate https://s3.amazonaws.com/influxdb/influxdb-0.10.0-1.x86_64.rpm
$ sudo yum localinstall influxdb-0.10.0-1.x86_64.rpm
$ sudo systemctl influxdb start

$ sudo netstat -antp | grep inf
tcp        0      0 127.0.0.1:8091          0.0.0.0:*               LISTEN      32063/influxd
tcp6       0      0 :::8083                 :::*                    LISTEN      32063/influxd
tcp6       0      0 :::8086                 :::*                    LISTEN      32063/influxd
tcp6       0      0 :::8088                 :::*                    LISTEN      32063/influxd

```



## 레퍼런스 ##

https://www.popit.kr/influxdb_telegraf_grafana_1/
