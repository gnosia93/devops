## 레퍼런스 ##

https://www.tutorialspoint.com/ansible/index.htm

https://serversforhackers.com/c/an-ansible-tutorial


/etc/ansible/hosts

[web]

192.168.29.223

192.168.29.142

192.168.29.145



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

##  ##
ansible.cfg 에서 ssh 설정 변경.
```
# uncomment this to disable SSH key host checking
host_key_checking = False
```




## 우분투에 ssh 설치하기 ##
ssh 모듈을 설치한 다음 데몬 상태를 확인하고 다시 ping.  이번에는 권한 에러가 발생한다. 

```
$ sudo apt-get install ssh 
$ service sshd status
$ ansible all -m ping

startup@startup:~/.ssh$ ansible web -m ping
192.168.29.223 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: Permission denied (publickey,password).\r\n",
    "unreachable": true
}
192.168.29.142 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: Permission denied (publickey,password).\r\n",
    "unreachable": true
}
```

```
<192.168.29.223> ESTABLISH SSH CONNECTION FOR USER: None
<192.168.29.223> SSH: EXEC ssh -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o ConnectTimeout=10 -o ControlPath=/home/startup/.ansible/cp/cb7d8b7841 192.168.29.223 '/bin/sh -c '"'"'echo ~ && sleep 0'"'"''
```
