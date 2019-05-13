

## 아파치 포트 변경 ##
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

```


## 방화벽 포트 오픈 ## 

```
[startup@startup conf]$ sudo firewall-cmd --permanent --add-port=9000/tcp
success
[startup@startup conf]$ sudo firewall-cmd --reload
```

## 레퍼런스 ##

https://www.server-world.info/en/note?os=CentOS_7&p=graphite

https://stackoverflow.com/questions/17079670/httpd-server-not-started-13permission-denied-make-sock-could-not-bind-to-ad

https://www.lesstif.com/pages/viewpage.action?pageId=22053128
