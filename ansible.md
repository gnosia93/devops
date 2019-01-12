## 레퍼런스 ##

https://www.tutorialspoint.com/ansible/index.htm

https://serversforhackers.com/c/an-ansible-tutorial

https://moonstrike.github.io/ansible/2016/09/09/Ansible-Basics.html

https://sysnet4admin.blogspot.com/2017/10/ansible-nginx_27.html#.XDlVUVwzYuU

https://blog.ssdnodes.com/blog/step-by-step-ansible-guide/

https://code-maven.com/install-and-configure-nginx-using-ansible



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
### 1. nginx 설치 ###
```
startup@startup:~$ ansible 192.168.29.223 -b -K -m apt -a 'name=nginx state=present update_cache=true' -u ansible
SUDO password:
192.168.29.223 | CHANGED => {
    "cache_update_time": 1547265344,
    "cache_updated": true,
    "changed": true,
    "stderr": "",
    "stderr_lines": [],
    "stdout": "Reading package lists...\nBuilding dependency tree...\nReading state information...\nThe following additional packages will be installed:\n  nginx-common nginx-core\nSuggested packages:\n  fcgiwrap nginx-doc\nThe following NEW packages will be installed:\n  nginx nginx-common nginx-core\n0 upgraded, 3 newly installed, 0 to remove and 673 not upgraded.\nNeed to get 459 kB of archives.\nAfter this operation, 1482 kB of additional disk space will be used.\nGet:1 http://kr.archive.ubuntu.com/ubuntu xenial-updates/main amd64 nginx-common all 1.10.3-0ubuntu0.16.04.3 [26.7 kB]\nGet:2 http://kr.archive.ubuntu.com/ubuntu xenial-updates/main amd64 nginx-core amd64 1.10.3-0ubuntu0.16.04.3 [429 kB]\nGet:3 http://kr.archive.ubuntu.com/ubuntu xenial-updates/main amd64 nginx all 1.10.3-0ubuntu0.16.04.3 [3506 B]\nPreconfiguring packages ...\nFetched 459 kB in 0s (1518 kB/s)\nSelecting previously unselected package nginx-common.\r\n(Reading database ... \r(Reading database ... 5%\r(Reading database ... 10%\r(Reading database ... 15%\r(Reading database ... 20%\r(Reading database ... 25%\r(Reading database ... 30%\r(Reading database ... 35%\r(Reading database ... 40%\r(Reading database ... 45%\r(Reading database ... 50%\r(Reading database ... 55%\r(Reading database ... 60%\r(Reading database ... 65%\r(Reading database ... 70%\r(Reading database ... 75%\r(Reading database ... 80%\r(Reading database ... 85%\r(Reading database ... 90%\r(Reading database ... 95%\r(Reading database ... 100%\r(Reading database ... 181587 files and directories currently installed.)\r\nPreparing to unpack .../nginx-common_1.10.3-0ubuntu0.16.04.3_all.deb ...\r\nUnpacking nginx-common (1.10.3-0ubuntu0.16.04.3) ...\r\nSelecting previously unselected package nginx-core.\r\nPreparing to unpack .../nginx-core_1.10.3-0ubuntu0.16.04.3_amd64.deb ...\r\nUnpacking nginx-core (1.10.3-0ubuntu0.16.04.3) ...\r\nSelecting previously unselected package nginx.\r\nPreparing to unpack .../nginx_1.10.3-0ubuntu0.16.04.3_all.deb ...\r\nUnpacking nginx (1.10.3-0ubuntu0.16.04.3) ...\r\nProcessing triggers for systemd (229-4ubuntu7) ...\r\nProcessing triggers for ureadahead (0.100.0-19) ...\r\nProcessing triggers for ufw (0.35-0ubuntu2) ...\r\nSetting up nginx-common (1.10.3-0ubuntu0.16.04.3) ...\r\nSetting up nginx-core (1.10.3-0ubuntu0.16.04.3) ...\r\nSetting up nginx (1.10.3-0ubuntu0.16.04.3) ...\r\nProcessing triggers for systemd (229-4ubuntu7) ...\r\nProcessing triggers for ureadahead (0.100.0-19) ...\r\nProcessing triggers for ufw (0.35-0ubuntu2) ...\r\n",
    "stdout_lines": [
        "Reading package lists...",
        "Building dependency tree...",
        "Reading state information...",
        "The following additional packages will be installed:",
        "  nginx-common nginx-core",
        "Suggested packages:",
        "  fcgiwrap nginx-doc",
        "The following NEW packages will be installed:",
        "  nginx nginx-common nginx-core",
        "0 upgraded, 3 newly installed, 0 to remove and 673 not upgraded.",
        "Need to get 459 kB of archives.",
        "After this operation, 1482 kB of additional disk space will be used.",
        "Get:1 http://kr.archive.ubuntu.com/ubuntu xenial-updates/main amd64 nginx-common all 1.10.3-0ubuntu0.16.04.3 [26.7 kB]",
        "Get:2 http://kr.archive.ubuntu.com/ubuntu xenial-updates/main amd64 nginx-core amd64 1.10.3-0ubuntu0.16.04.3 [429 kB]",
        "Get:3 http://kr.archive.ubuntu.com/ubuntu xenial-updates/main amd64 nginx all 1.10.3-0ubuntu0.16.04.3 [3506 B]",
        "Preconfiguring packages ...",
        "Fetched 459 kB in 0s (1518 kB/s)",
        "Selecting previously unselected package nginx-common.",
        "(Reading database ... ",
        "(Reading database ... 5%",
        "(Reading database ... 10%",
        "(Reading database ... 15%",
        "(Reading database ... 20%",
        "(Reading database ... 25%",
        "(Reading database ... 30%",
        "(Reading database ... 35%",
        "(Reading database ... 40%",
        "(Reading database ... 45%",
        "(Reading database ... 50%",
        "(Reading database ... 55%",
        "(Reading database ... 60%",
        "(Reading database ... 65%",
        "(Reading database ... 70%",
        "(Reading database ... 75%",
        "(Reading database ... 80%",
        "(Reading database ... 85%",
        "(Reading database ... 90%",
        "(Reading database ... 95%",
        "(Reading database ... 100%",
        "(Reading database ... 181587 files and directories currently installed.)",
        "Preparing to unpack .../nginx-common_1.10.3-0ubuntu0.16.04.3_all.deb ...",
        "Unpacking nginx-common (1.10.3-0ubuntu0.16.04.3) ...",
        "Selecting previously unselected package nginx-core.",
        "Preparing to unpack .../nginx-core_1.10.3-0ubuntu0.16.04.3_amd64.deb ...",
        "Unpacking nginx-core (1.10.3-0ubuntu0.16.04.3) ...",
        "Selecting previously unselected package nginx.",
        "Preparing to unpack .../nginx_1.10.3-0ubuntu0.16.04.3_all.deb ...",
        "Unpacking nginx (1.10.3-0ubuntu0.16.04.3) ...",
        "Processing triggers for systemd (229-4ubuntu7) ...",
        "Processing triggers for ureadahead (0.100.0-19) ...",
        "Processing triggers for ufw (0.35-0ubuntu2) ...",
        "Setting up nginx-common (1.10.3-0ubuntu0.16.04.3) ...",
        "Setting up nginx-core (1.10.3-0ubuntu0.16.04.3) ...",
        "Setting up nginx (1.10.3-0ubuntu0.16.04.3) ...",
        "Processing triggers for systemd (229-4ubuntu7) ...",
        "Processing triggers for ureadahead (0.100.0-19) ...",
        "Processing triggers for ufw (0.35-0ubuntu2) ..."
    ]
}

```

동일한 명령어를 다시 실행하면 "changed" 는 false 로 나타난다. (ansible 멱등성)
```
startup@startup:~$ ansible 192.168.29.223 -b -K -m apt -a 'name=nginx state=present update_cache=true' -u ansible
SUDO password:
192.168.29.223 | SUCCESS => {
    "cache_update_time": 1547265437,
    "cache_updated": true,
    "changed": false
}

```

### 2. nginx 인스톨 / 동작 여부 확인 ###

rc = 0 이다. 

```
startup@startup:~$ ansible web -b -K -m shell -a 'service nginx status' -u ansible
SUDO password:
 [WARNING]: Consider using the service module rather than running service.  If you need to use command because service
is insufficient you can add warn=False to this command task or set command_warnings=False in ansible.cfg to get rid of
this message.

192.168.29.223 | CHANGED | rc=0 >>
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since 토 2019-01-12 13:31:27 KST; 12min ago
  Process: 4816 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
  Process: 4812 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
 Main PID: 4819 (nginx)
   CGroup: /system.slice/nginx.service
           ├─4819 nginx: master process /usr/sbin/nginx -g daemon on; master_process on
           ├─4820 nginx: worker process
           └─4821 nginx: worker process

 1월 12 13:31:27 ubuntu1 systemd[1]: Starting A high performance web server and a reverse proxy server...
 1월 12 13:31:27 ubuntu1 systemd[1]: Started A high performance web server and a reverse proxy server.

192.168.29.145 | CHANGED | rc=0 >>
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since 토 2019-01-12 13:31:38 KST; 12min ago
 Main PID: 4058 (nginx)
   CGroup: /system.slice/nginx.service
           ├─4058 nginx: master process /usr/sbin/nginx -g daemon on; master_process on
           ├─4059 nginx: worker process
           └─4060 nginx: worker process

 1월 12 13:31:38 ubuntu2 systemd[1]: Starting A high performance web server and a reverse proxy server...
 1월 12 13:31:38 ubuntu2 systemd[1]: Started A high performance web server and a reverse proxy server.

192.168.29.142 | CHANGED | rc=0 >>
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since 토 2019-01-12 13:31:38 KST; 12min ago
 Main PID: 4042 (nginx)
   CGroup: /system.slice/nginx.service
           ├─4042 nginx: master process /usr/sbin/nginx -g daemon on; master_process on
           ├─4043 nginx: worker process
           └─4044 nginx: worker process

 1월 12 13:31:38 ubuntu2 systemd[1]: Starting A high performance web server and a reverse proxy server...
 1월 12 13:31:38 ubuntu2 systemd[1]: Started A high performance web server and a reverse proxy server.

startup@startup:~$

```

### 3. nginx 정지 ###
```
ansible 192.168.29.223 -b -K -m service -a 'name=nginx state=stopped' -u ansible
```

### 4. nginx 삭제 ###

삭제는 state 값으로 조정하고, autoremove 는 의존관계를 제거하는 옵션이다. 

```
ansible 192.168.29.223 -b -K -m apt -a 'name=nginx state=absent autoremove=yes' -u ansible
```


## PlayBook ##

## playbook 기초 ##

nginx_install.yml 의 내용이다. 

```
- hosts: web
  gather_facts: yes
  remote_user: ansible
  become: yes
#  ask_become_pass : true             ask-become-pass 는 play 에 사용할 수 없는 키워드 이다. 

  tasks:
     - name: install nginx to web
       apt :
          name: nginx
          state: present
     - name: start nginx
       service :
          name: nginx
          state: started
                   
          
```


-K 는 꼭 대문자로 써줘야 한다. 
```
startup@startup:~/ansible/nginx$ ansible-playbook nginx_install.yml -K
SUDO password:

PLAY [web] *************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************
ok: [192.168.29.223]
ok: [192.168.29.145]
ok: [192.168.29.142]

TASK [install nginx to web] ********************************************************************************************************
ok: [192.168.29.142]
ok: [192.168.29.145]
ok: [192.168.29.223]

TASK [start nginx] *****************************************************************************************************************
ok: [192.168.29.142]
ok: [192.168.29.145]
ok: [192.168.29.223]

PLAY RECAP *************************************************************************************************************************
192.168.29.142             : ok=3    changed=0    unreachable=0    failed=0
192.168.29.145             : ok=3    changed=0    unreachable=0    failed=0
192.168.29.223             : ok=3    changed=0    unreachable=0    failed=0


```

```
조건분기.
https://sysnet4admin.blogspot.com/2017/10/ansible-nginx_27.html#.XDlVUVwzYuU


loop / delay..

try catch.

event handler.

```


