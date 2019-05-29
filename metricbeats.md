## 설치 ##

```
$ sudo yum install metricbeat
```


$ sudo vi /etc/metricbeats/metricbeat.yml
```
57 #============================== Kibana =====================================
58
59 # Starting with Beats version 6.0.0, the dashboards are loaded via the Kibana API.
60 # This requires a Kibana endpoint configuration.
61 setup.kibana:
62
63   # Kibana Host
64   # Scheme and port can be left out and will be set to the default (http and 5601)
65   # In case you specify and additional path, the scheme is required: http://localhost:5601/path
66   # IPv6 addresses should always be defined as: https://[2001:db8::1]:5601
67   host: "localhost:5601"
68
69   # Kibana Space ID
70   # ID of the Kibana Space into which the dashboards should be loaded. By default,
71   # the Default Space will be used.
72   #space.id:


87 #================================ Outputs =====================================
88
89 # Configure what output to use when sending the data collected by the beat.
90
91 #-------------------------- Elasticsearch output ------------------------------
92 output.elasticsearch:
93   # Array of hosts to connect to.
94   hosts: ["localhost:9200"]
95
96   # Enabled ilm (beta) to use index lifecycle management instead daily indices.
97   #ilm.enabled: false
98
99   # Optional protocol and basic auth credentials.
100   #protocol: "https"
101   #username: "elastic"
102   #password: "changeme"
103
```

## elasticsearch index  ##

```
$ curl localhost:9200/_cat/indices?v | grep metricbeat

 % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 12573  100 12573yellow open   metricbeat-6.8.0-2019.05.29     BlphpxapQZmN0_VHu-d1wg   1   1        145            0    547.9kb        547.9kb
    0     0   109k      0 --:--:-- --:--:-- --:--:--  110k
```


## 키바나 대시보드 설치 ##

```
$ sudo metricbeat setup --dashboards
Loading dashboards (Kibana must be running and reachable)

Loaded dashboards
```


## 레퍼런스 ##

https://www.server-world.info/en/note?os=CentOS_7&p=elasticstack6&f=5
