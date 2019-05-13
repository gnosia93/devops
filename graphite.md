

## 아파치 포트 변경 ##

SELinux 가 Enabe 되어 있는 경우 아파치에서 바인딩 되는 포트는 정해져 있다. (아래 레퍼런스 참조)

```
$ sudo vi /etc/httpd/conf/httpd.conf

#
# Listen: Allows you to bind Apache to specific IP addresses and/or
# ports, instead of the default. See also the <VirtualHost>
# directive.
#
# Change this to Listen on specific IP addresses as shown below to
# prevent Apache from glomming onto all bound IP addresses.
#
#Listen 12.34.56.78:80
Listen 9000
Listen 9002
```

## SELinux 포트 오픈 ##
```
$ sudo yum -y install policycoreutils-python
$ sudo semanage port -a -t http_port_t -p tcp 9002
```

## 방화벽 포트 오픈 ## 

```
$ sudo firewall-cmd --permanent --add-port=9000/tcp
success

$ sudo firewall-cmd --permanent --add-port=9002/tcp
success

$ sudo firewall-cmd --reload
```

## 레퍼런스 ##

https://www.server-world.info/en/note?os=CentOS_7&p=graphite

https://stackoverflow.com/questions/17079670/httpd-server-not-started-13permission-denied-make-sock-could-not-bind-to-ad

https://www.lesstif.com/pages/viewpage.action?pageId=22053128
