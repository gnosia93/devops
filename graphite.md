## Graphite  ##

https://www.server-world.info/en/note?os=CentOS_7&p=graphite


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

## 버추얼 호스트 설정 ##

/etc/httpd/conf.d/graphite-web.conf 파일을 아래와 같이 수정한다. 

포트 기반의 버추얼 호스트 설정을 위해 VirtualHost 태그 부분에 192.168.29.106:9002 로 설정하였고, 

접근 가능한 IP 대역을 Require ip 192.168.29.0/24 로 설정하였다. 

웹 브라우저에서 http://192.168.29.106:9002 로 접속하면 graphite 화면을 볼 수 있다. 

```
# Graphite Web Basic mod_wsgi vhost

<VirtualHost 192.168.29.106:9002>
  #  ServerName graphite-web
    DocumentRoot "/usr/share/graphite/webapp"
    ErrorLog /var/log/httpd/graphite-web-error.log
    CustomLog /var/log/httpd/graphite-web-access.log common

    # Header set Access-Control-Allow-Origin "*"
    # Header set Access-Control-Allow-Methods "GET, OPTIONS"
    # Header set Access-Control-Allow-Headers "origin, authorization, accept"
    # Header set Access-Control-Allow-Credentials true

    WSGIScriptAlias / /usr/share/graphite/graphite-web.wsgi
    WSGIImportScript /usr/share/graphite/graphite-web.wsgi process-group=%{GLOBAL} application-group=%{GLOBAL}

    <Location "/content/">
        SetHandler None
    </Location>

    Alias /media/ "/usr/lib/python2.7/site-packages/django/contrib/admin/media/"
    <Location "/media/">
        SetHandler None
    </Location>

   <Directory "/usr/share/graphite/">
       <IfModule mod_authz_core.c>
           # Apache 2.4
           Require local
           Require ip 192.168.29.0/24
       </IfModule>
       <IfModule !mod_authz_core.c>
           # Apache 2.2
           Order Deny,Allow
           Deny from all
           Allow from 127.0.0.1
           Allow from ::1
       </IfModule>
   </Directory>
</VirtualHost>


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

https://pshcode.tistory.com/88
