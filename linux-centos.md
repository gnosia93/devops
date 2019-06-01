### firewalld ###

```
$ systemctl status firewalld
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
   Active: active (running) since 월 2019-05-20 20:34:52 KST; 1 weeks 4 days ago
     Docs: man:firewalld(1)
 Main PID: 5163 (firewalld)
    Tasks: 2
   Memory: 26.0M
   CGroup: /system.slice/firewalld.service
           └─5163 /usr/bin/python -Es /usr/sbin/firewalld --nofork --nopid

 5월 29 23:46:55 startup firewalld[5163]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -C F...in?).
 5월 29 23:46:55 startup firewalld[5163]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t nat -C PRER...name.
 5월 29 23:46:55 startup firewalld[5163]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t nat -C OUTP...name.
 5월 29 23:46:55 startup firewalld[5163]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -C F...name.
 5월 29 23:46:55 startup firewalld[5163]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -C F...in?).
 5월 29 23:46:55 startup firewalld[5163]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -C F...name.
 5월 29 23:46:55 startup firewalld[5163]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -D FORWARD -i ...in?).
 5월 29 23:46:55 startup firewalld[5163]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -n -...name.
 5월 29 23:46:55 startup firewalld[5163]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -C D...in?).
 5월 29 23:46:55 startup firewalld[5163]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w2 -t filter -C F...name.
Hint: Some lines were ellipsized, use -l to show in full.


$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: wlp0s20f0u1
  sources:
  services: ssh dhcpv6-client http https
  ports: 9090/tcp 9200/tcp 9300/tcp 8080/tcp 8443/tcp 88/tcp 8001/tcp 9000/tcp 9002/tcp 3000/tcp 8083/tcp 8086/tcp 3389/tcp
  protocols:
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

$ sudo firewall-cmd --permanent --add-port=5632/tcp
success

$ sudo firewall-cmd --reload
```
