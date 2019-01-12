## 레퍼런스 ##

https://www.tutorialspoint.com/ansible/index.htm

https://serversforhackers.com/c/an-ansible-tutorial


## ping ##

ssh 설정이 되어 있지 않아서 에러가 발생한다. 

```
$ ansible all -m ping
192.168.29.223 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: ssh: connect to host 192.168.29.223 port 22: Connection refused\r\n",
    "unreachable": true
}
192.168.29.142 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: ssh: connect to host 192.168.29.142 port 22: Connection refused\r\n",
    "unreachable": true
}

```
