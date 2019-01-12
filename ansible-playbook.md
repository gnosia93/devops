
## PlayBook ##

### nginx 설치 ###

nginx_install.yml 으로 설치후 nginx 를 stop 하기 위해 notify 하고 있다.

```
- hosts: web
  gather_facts: yes
  remote_user: ansible
  become: yes
#  ask_become_pass : true

  tasks:
     - name: install nginx to web
       apt :
          name: nginx
          state: present
       notify:
          - stop nginx after install

  handlers:
     - name: stop nginx after install
       service:
          name: nginx
          state: stopped
          
```


-K 는 꼭 대문자로 써줘야 한다. 
```
$ ansible-playbook nginx_install.yml -K
SUDO password:

PLAY [web] *************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************
ok: [192.168.29.223]
ok: [192.168.29.142]
ok: [192.168.29.145]

TASK [install nginx to web] ********************************************************************************************************
changed: [192.168.29.145]
changed: [192.168.29.223]
changed: [192.168.29.142]

RUNNING HANDLER [stop nginx after install] *****************************************************************************************
changed: [192.168.29.223]
changed: [192.168.29.142]
changed: [192.168.29.145]

PLAY RECAP *************************************************************************************************************************
192.168.29.142             : ok=3    changed=2    unreachable=0    failed=0
192.168.29.145             : ok=3    changed=2    unreachable=0    failed=0
192.168.29.223             : ok=3    changed=2    unreachable=0    failed=0

```


### nginx 삭제 ###
```
- hosts: web
  remote_user: ansible
  become: yes

  tasks:
    - name: remove nginx
      apt:
        name: nginx
        state: absent
        autoremove : yes
```

```
$ ansible-playbook nginx_remove.yml -K
SUDO password:

PLAY [web] *************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************
ok: [192.168.29.142]
ok: [192.168.29.145]
ok: [192.168.29.223]

TASK [remove nginx] ****************************************************************************************************************
changed: [192.168.29.223]
changed: [192.168.29.145]
changed: [192.168.29.142]

PLAY RECAP *************************************************************************************************************************
192.168.29.142             : ok=2    changed=1    unreachable=0    failed=0
192.168.29.145             : ok=2    changed=1    unreachable=0    failed=0
192.168.29.223             : ok=2    changed=1    unreachable=0    failed=0

```


```

```
조건분기.
https://sysnet4admin.blogspot.com/2017/10/ansible-nginx_27.html#.XDlVUVwzYuU


loop / delay..

try catch.

event handler.

```
