## IP 수동 설정 ##

/etc/network/interfaces
```
# interfaces(5) file used by ifup(8) and ifdown(8)
auto lo
iface lo inet loopback
auto enp0s3
iface enp0s3 inet static
address 10.0.2.10
netmask 255.255.255.0
gateway 10.0.2.2
dns-nameservers 8.8.8.8
```
네트워크 재시작.
```
systemctl restart networking.service
```


## DHCP 설정 ##
```
# The primary network interface
auto enp0s3
iface enp0s3 inet dhcp
```
