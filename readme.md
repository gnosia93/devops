## OS ##

[CentOS ](https://github.com/gnosia93/devops/blob/master/os-cmd.md)

[MacOS](https://techsviewer.com/install-macos-10-14-mojave-virtualbox-windows/)


## devops Interview ##

https://www.youtube.com/watch?v=clZgb8GA6xI


## Cloud ##

https://opentutorials.org/course/2717/11268

## Cache ##

[Redis](https://github.com/gnosia93/devops/blob/master/redis.md)


확장성 있는 웹 아키텍처와 분산 시스템

https://d2.naver.com/helloworld/206816


## Security ##

https://en.wikipedia.org/wiki/Key_management

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

[E.L.K Install](https://github.com/gnosia93/devops/blob/master/e.l.k.md)

[ElasticSearch Admin](https://github.com/gnosia93/devops/blob/master/elastic-admin.md)



아키텍처..
https://medium.com/chequer/elkr-elasticsearch-logstash-kibana-redis-%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%A1%9C%EA%B7%B8%EB%B6%84%EC%84%9D-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0-f3dd9dfae622


# 모니터링 #

[telegraf](https://www.popit.kr/influxdb_telegraf_grafana_2/)

https://github.com/scouter-project/scouter

http://gblee1987.tistory.com/35

## Linux Admin ##

[Centos](https://github.com/gnosia93/devops/blob/master/linux-centos.md)

[Ubuntu](https://github.com/gnosia93/devops/blob/master/linux-ubuntu.md)

[KVM install on Cent](https://www.linuxtechi.com/install-kvm-hypervisor-on-centos-7-and-rhel-7/)

## Ansible ##

[Setup](https://github.com/gnosia93/devops/blob/master/ansible.md)

[Adhoc](https://github.com/gnosia93/devops/blob/master/ansible-adhoc.md)

[Playbook](https://github.com/gnosia93/devops/blob/master/ansible-playbook.md)

[Playbook Example](https://github.com/gnosia93/devops/blob/master/ansible-playbook-example.md)

https://code-maven.com/setup-for-learning-ansible


## Kubernetes ##

https://linuxconfig.org/how-to-install-kubernetes-on-ubuntu-18-04-bionic-beaver-linux    -- 설치가이드.



[Ansible Install](https://github.com/gnosia93/devops/blob/master/k8.md)

https://kubernetes.io/ko/docs/tutorials/

https://www.howtoforge.com/tutorial/centos-kubernetes-docker-cluster/


## OpenShift ##

* [인스톨](https://github.com/gnosia93/devops/blob/master/openshift-install.md)

* [OKD](https://docs.okd.io/3.11/welcome/index.html)

* [OpenShift Youtube](https://www.youtube.com/user/rhopenshift/videos)



-- 꼭 다 익혀야 한다.
https://www.linux.com/blog/learn/chapter/Intro-to-Kubernetes/2017/5/set-cicd-pipeline-kubernetes-part-1-overview

## Jenkins ##

https://jenkins.io/doc/book/pipeline/

http://wiki.rockplace.co.kr/pages/viewpage.action?pageId=3870355

[젠킨스튜토리얼](https://www.youtube.com/watch?v=89yWXXIOisk)

[젠킨스 JOB 모니터링 - catlight](https://catlight.io/)


## SW Stack ##

[Nginx](https://github.com/gnosia93/devops/blob/master/nginx.md)



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


