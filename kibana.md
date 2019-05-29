## 설치 ##

```

$ systemctl status kibana
● kibana.service - Kibana
   Loaded: loaded (/etc/systemd/system/kibana.service; enabled; vendor preset: disabled)
   Active: active (running) since 월 2019-05-20 20:34:52 KST; 1 weeks 1 days ago
 Main PID: 5053 (node)
    Tasks: 11
   Memory: 148.3M
   CGroup: /system.slice/kibana.service
           └─5053 /usr/share/kibana/bin/../node/bin/node --no-warnings --max-http-header-size=65536 /usr/share/kibana/bin/../src/cli -c /etc/kibana/kibana.yml

```

