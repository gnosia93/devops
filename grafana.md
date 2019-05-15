## 설치 ##

```
$ wget https://grafanarel.s3.amazonaws.com/builds/grafana-4.1.2-1486989747.linux-x64.tar.gz
$ tar zxvf grafana-4.1.2-1486989747.linux-x64.tar.gz
$ cd grafana-4.1.2-1486989747
$ bin/grafana-server

$ sudo firewall-cmd --permanent --add-port=3000/tcp
success
$ sudo firewall-cmd --reload

```

브라우저로 http://startup:3000 를 접속하여 테스트 (디폴트 패스워드는 admin/admin)

## 설정 ##




## 레퍼런스 ##

https://blog.vpscheap.net/how-to-setup-grafana-in-centos-7/

https://grafana.com/docs/
