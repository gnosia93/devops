## CI-CD ##

* [JENKINS GitHub Webhook](https://github.com/gnosia93/devops/blob/master/jenkins-github-webhook.md)

* [JENKINS PipeLine](https://github.com/gnosia93/devops/blob/master/jenkins-pipeline.md)

* [JENKINS Tutorial](https://www.tutorialspoint.com/jenkins/index.htm)

* [CD/CD on K8S /w Jenkins](https://medium.com/containerum/configuring-ci-cd-on-kubernetes-with-jenkins-89eab7234270)


## Test ##

https://martinfowler.com/articles/microservice-testing/#testing-end-to-end-tips


# 로그 관리 #

logback 에서 kafka 로 메시지 보내기. 

http://gyrfalcon.tistory.com/entry/Kafka-Kafka%EB%A1%9C-Log%EB%A5%BC-%EB%B3%B4%EB%82%B4%EB%8A%94-%EB%B0%A9%EB%B2%95%EB%93%A4

http://goddaehee.tistory.com/45


아키텍처..
https://medium.com/chequer/elkr-elasticsearch-logstash-kibana-redis-%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%A1%9C%EA%B7%B8%EB%B6%84%EC%84%9D-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0-f3dd9dfae622


# 모니터링 #

https://github.com/scouter-project/scouter

http://gblee1987.tistory.com/35

## Linux Admin ##

[Centos](https://github.com/gnosia93/devops/blob/master/linux-centos.md)

[Ubuntu](https://github.com/gnosia93/devops/blob/master/linux-ubuntu.md)

## Ansible ##

[Setup](https://github.com/gnosia93/devops/blob/master/ansible.md)

[Adhoc](https://github.com/gnosia93/devops/blob/master/ansible-adhoc.md)

[Playbook](https://github.com/gnosia93/devops/blob/master/ansible-playbook.md)

https://code-maven.com/setup-for-learning-ansible


## Kubernetes ##
[Ansible Install](https://github.com/gnosia93/devops/blob/master/k8.md)

https://kubernetes.io/ko/docs/tutorials/

https://www.howtoforge.com/tutorial/centos-kubernetes-docker-cluster/


-- 꼭 다 익혀야 한다.
https://www.linux.com/blog/learn/chapter/Intro-to-Kubernetes/2017/5/set-cicd-pipeline-kubernetes-part-1-overview

## Jenkins ##

https://jenkins.io/doc/book/pipeline/

http://wiki.rockplace.co.kr/pages/viewpage.action?pageId=3870355



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
