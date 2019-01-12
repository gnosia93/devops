## 레퍼런스 ##

https://www.tutorialspoint.com/ansible/index.htm

https://serversforhackers.com/c/an-ansible-tutorial


## Initial Setup ##

https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04


### 1. ansible 용 리모트 유저 생성 ###

관리 대상 서버인 리모트 서버들에 ansible 이라는 유저를 생성한다. 

```
$ sudo useradd -m -G sudo ansible
$ passwd ansible
$ su - ansible
ansible@ubuntu1:~$ id
uid=1001(ansible) gid=1001(ansible) 그룹들=1001(ansible),27(sudo)
```

### 2. ssh 데몬 설치 ###

관리 대상 서버에 ssh 데몬을 설치한다. 아래는 우분투에서 sshd 설치하는 방법이다. 
```
$ sudo apt-get install ssh 
$ service sshd status
$ ansible all -m ping
```


### 3. 관리 서버에 ssh-keygen ###

관리 서버에 ssh 키를 생성한다. 
```
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/startup/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/startup/.ssh/id_rsa.
Your public key has been saved in /home/startup/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:42cX+8r/wHEqXPf08uDOk2//HUUTNqsnhL7FqABZ1xE startup@startup
The key's randomart image is:
+---[RSA 2048]----+
|       . ..Eo  + |
|      o .  .. . +|
|     o     . . o.|
|      .   . + ...|
|       .S  o.=o.=|
|       .....o=o*+|
|        ..o.= *oo|
|         o o =o=+|
|            o+*=X|
+----[SHA256]-----+
startup@startup:~$

```

### 4. Pub Key Copy ###

리모트 서버에 ssh pub key 를 카피한다. 
```
$ which ssh-copy-id
/usr/bin/ssh-copy-id
$ ssh-copy-id ansible@192.168.29.223
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/startup/.ssh/id_rsa.pu                            b"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any tha                            t are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it i                            s to install the new keys
ansible@192.168.29.223's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'ansible@192.168.29.223'"
and check to make sure that only the key(s) you wanted were added.
```


## ansible 설치 및 설정 ##

ansible.cfg 에서 ssh 설정 변경.
```
# uncomment this to disable SSH key host checking
host_key_checking = False
```

인벤토리 파일에 관리 대상 서버 목록 등록
```
$ cd /etc/ansible
$ cat hosts
[web]
192.168.29.223
192.168.29.142
192.168.29.145
```


## Ansible 테스트 ##

### ping ###
-u 옵션을 이용하여 ssh 로 로그인 할 유저를 명시한다. default 는 root 이다. 

145 번 서버는 리모트 서버에 ansible 계정이 없거나 pub key 가 복사되지 않아서 발생하는 에러이다.

142 번 서버는 현재 shutdown 되어 있다. 


```
$ ansible web -m ping -u ansible
192.168.29.145 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: Permission denied (publickey,password).\r\n",
    "unreachable": true
}
192.168.29.223 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
192.168.29.142 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: ssh: connect to host 192.168.29.142 port 22: No route to host\r\n",
    "unreachable": true
}
```

### Reboot ###

```
~$ ansible all -a "/sbin/reboot" -u ansible --become -K
```


## Facts ##

```
$ ansible 192.168.29.223 -m setup -u ansible
```

## Adhoc ##
### nginx 설치 ###
```
11
```



## PlayBook ##
```
조건분기.
https://sysnet4admin.blogspot.com/2017/10/ansible-nginx_27.html#.XDlVUVwzYuU
```


