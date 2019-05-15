## 설치 ##

https://grafana.com/docs/installation/rpm/

```
$ sudo yum install https://dl.grafana.com/oss/release/grafana-5.4.2-1.x86_64.rpm
$ sudo yum install initscripts 
$ sudo yum install fontconfig
$ sudo yum install freetype*
$ sudo yum install urw-fonts

$ systemctl daemon-reload
$ systemctl start grafana-server
$ systemctl status grafana-server
$ sudo systemctl enable grafana-server.service

$ sudo firewall-cmd --permanent --add-port=3000/tcp
success
$ sudo firewall-cmd --reload

```

브라우저로 http://startup:3000 를 접속하여 테스트 (디폴트 패스워드는 admin/admin)

## 설정 ##

https://grafana.com/docs/features/datasources/graphite/




## 레퍼런스 ##



https://grafana.com/docs/
