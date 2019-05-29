## 설치 ##

```
$ sudo yum install metricbeat

```

## 정상 동작여부 확인 ##

```
$ curl localhost:9200/_cat/indices?v | grep metricbeat

 % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 12573  100 12573yellow open   metricbeat-6.8.0-2019.05.29     BlphpxapQZmN0_VHu-d1wg   1   1        145            0    547.9kb        547.9kb
    0     0   109k      0 --:--:-- --:--:-- --:--:--  110k


```



## 레퍼런스 ##

https://www.server-world.info/en/note?os=CentOS_7&p=elasticstack6&f=5
