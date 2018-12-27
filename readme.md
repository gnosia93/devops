## Docker ##

### Docker Log 관리 ###

아래는 docker 컨테이들의 기본 로그 파일 위치이다. 

```
root@startup:/var/lib/docker/containers# pwd
/var/lib/docker/containers

```

http://egloos.zum.com/mcchae/v/11259352


### ORACLE JDK 받는 방법 ###
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


### Elastic Search Docker Image ###
https://hub.docker.com/_/elasticsearch

