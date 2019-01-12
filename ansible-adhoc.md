
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
