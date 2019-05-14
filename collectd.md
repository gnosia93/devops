# 2. Collectd 설정 #

아래와 같이 collectd 와 collectd mysql plugin 을 설치해 준다. 

```
$ yum update
$ yum upgrade
$ yum install epel-release 
$ sudo yum install collectd
$ sudo yum install collectd-mysql
```

collectd.conf 파일을 열어 적당히 편집해 준다. 
```
$ sudo vi /etc/collectd.conf
```


## 레퍼런스 ##

https://collectd.org/

https://linuxadmin.io/collectd-install-centos-7/

https://www.digitalocean.com/community/tutorials/how-to-configure-collectd-to-gather-system-metrics-for-graphite-on-ubuntu-14-04

https://collectd.org/wiki/index.php/Plugin:MySQL#Description

https://saksin.tistory.com/m/1087?category=396744

# 3. Graphana 설정 #
