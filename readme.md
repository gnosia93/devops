## Linux Admin ##

[Centos](https://github.com/gnosia93/devops/blob/master/linux-centos.md)

[Ubuntu](https://github.com/gnosia93/devops/blob/master/linux-ubuntu.md)

## Ansible ##

[Setup](https://github.com/gnosia93/devops/blob/master/ansible.md)

[Adhoc](https://github.com/gnosia93/devops/blob/master/ansible-adhoc.md)

[Playbook](https://github.com/gnosia93/devops/blob/master/ansible-playbook.md)


## Kubernetes ##
[Ansible Install](https://github.com/gnosia93/devops/blob/master/k8.md)

https://github.com/gnosia93/devops/blob/master/kubernetes.md

## Docker ##

https://github.com/gnosia93/devops/blob/master/docker.md


## ubuntu ##
https://github.com/gnosia93/devops/blob/master/ubuntu.md



#### ocker Log 관리 ####

아래는 docker 컨테이들의 기본 로그 파일 위치이다. 

```
root@startup:/var/lib/docker/containers# pwd
/var/lib/docker/containers

```
http://egloos.zum.com/mcchae/v/11259352

#### ORACLE JDK 받는 방법 ####
```
FROM ubuntu:16.04

RUN apt-get update && \
    apt-get install -y --no-install-recommends && \
    apt-get --purge -y remove openjdk* && \
    echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections && \
    echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" > /etc/apt/sources.list.d/webupd8team-java-trusty.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 && \
    apt-get update && \
    apt-get install -y --no-install-recommends oracle-java8-installer oracle-java8-set-default && \
    apt-get install -y git curl maven vim && \
    apt-get clean all

```


### Elastic Search / Kibana ###
https://hub.docker.com/_/elasticsearch
https://hub.docker.com/_/kibana
```
startup@startup:~$ docker pull elasticsearch:6.5.4
startup@startup:~$ docker network create devops
b8ac03b72e4bf3b1c65ed85bca8bd18c928661077ccff71c93da279b44d6a637
startup@startup:~$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
f224bae62d12        bridge              bridge              local
b8ac03b72e4b        devops              bridge              local
650c35516e16        host                host                local
bc39fdfbfff7        none                null                local
startup@startup:~$ docker run -d --name elasticsearch --net devops -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:6.5.4
06883f91badbcccd265ca13b0ffa4fc2a15da950a8d2df7c42ff49bf1a7c53a0
startup@startup:~$ docker ps -a
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                                              NAMES
06883f91badb        elasticsearch:6.5.4   "/usr/local/bin/dock…"   3 seconds ago       Up 2 seconds        0.0.0.0:9200->9200/tcp, 0.0.0.0:9300->9300/tcp     elasticsearch
d1c793065349        jenkins:latest        "/sbin/tini -- /usr/…"   28 minutes ago      Up 28 minutes       0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp   jenkins


startup@startup:~$ docker pull kibana:6.5.4
startup@startup:~$ docker run -d --name kibana --net devops -p 5601:5601 kibana:6.5.4
d434669240de15bf9f693d2c18c7b10526b545a832d43b8eee256f02d096af30
startup@startup:~$ docker ps -a
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                                              NAMES
d434669240de        kibana:6.5.4          "/usr/local/bin/kiba…"   3 seconds ago       Up 2 seconds        0.0.0.0:5601->5601/tcp                             kibana
06883f91badb        elasticsearch:6.5.4   "/usr/local/bin/dock…"   14 minutes ago      Up 14 minutes       0.0.0.0:9200->9200/tcp, 0.0.0.0:9300->9300/tcp     elasticsearch
d1c793065349        jenkins:latest        "/sbin/tini -- /usr/…"   42 minutes ago      Up 42 minutes       0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp   jenkins



```
