
## 설치 ##

최신버전 정보는 아래에서 확인할 수 있다. 

https://github.com/openshift/origin/releases

또한 github 에서는 소소 코드 또한 볼 수 있다 .. https://github.com/openshift/origin/tree/v3.11.0 


```
$ wget https://artifacts-openshift-release-3-11.svc.ci.openshift.org/zips/openshift-origin-server-v3.11.0-d0c29df-98-linux-64bit.tar.gz
$ tar xvfz openshift-origin-server-v3.11.0-d0c29df-98-linux-64bit.tar.gz
$ cd openshift-origin-server-v3.11.0-d0c29df-98-linux-64bit
$ sudo cp openshift oc kubectl /usr/local/bin
$ sudo firewall-cmd --add-port=8443/tcp --permanent
$ sudo firewall-cmd --reload
$ oc cluster up
```


## 에러1 ##
```
$ sudo oc cluster up
Getting a Docker client ...
Checking if image openshift/origin-control-plane:v3.11 is available ...
Pulling image openshift/origin-control-plane:v3.11
E0215 08:37:21.013595    3735 helper.go:173] Reading docker config from /root/.docker/config.json failed: open /root/.docker/config.json: no such file or directory, will attempt to pull image docker.io/openshift/origin-control-plane:v3.11 anonymously
Pulled 1/5 layers, 21% complete
Pulled 2/5 layers, 49% complete
Pulled 3/5 layers, 63% complete
Pulled 4/5 layers, 94% complete
Pulled 5/5 layers, 100% complete
Extracting
Image pull complete
Pulling image openshift/origin-cli:v3.11
E0215 08:38:07.641751    3735 helper.go:173] Reading docker config from /root/.docker/config.json failed: open /root/.docker/config.json: no such file or directory, will attempt to pull image docker.io/openshift/origin-cli:v3.11 anonymously
Image pull complete
Pulling image openshift/origin-node:v3.11
E0215 08:38:11.172065    3735 helper.go:173] Reading docker config from /root/.docker/config.json failed: open /root/.docker/config.json: no such file or directory, will attempt to pull image docker.io/openshift/origin-node:v3.11 anonymously
Pulled 5/6 layers, 85% complete
Pulled 6/6 layers, 100% complete
Extracting
Image pull complete
Checking type of volume mount ...
Determining server IP ...
Checking if OpenShift is already running ...
Checking for supported Docker version (=>1.22) ...
Checking if insecured registry is configured properly in Docker ...
error: did not detect an --insecure-registry argument on the Docker daemon

```

위와 같이 insecure-registry 관련 에러가 발생하는 경우, 아래 내용을 실행한다. 
```
sudo sysctl -w net.ipv4.ip_forward=1
sudo su

cat<<EOF>> /etc/docker/daemon.json
{
    "insecure-registries" : ["172.30.0.0/16"]
}
EOF

exit

sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 클래스터 실행하기 ##


```
$ sudo firewall-cmd --add-port=8443/tcp --permanent
$ firewall-cmd --reload
$ sudo usermod -a -G docker startup
```

오픈 쉬프트는 root 권한 실행을 금지하고 있다. 일반 유저로 oc 를 실행해야 한다. 

상기 스크립트에서 보이는 바와 같이 startup 유저에 docker 그룹을 추가해 주었다. (sudo를 사용하지 않기 위해) 

```
# cd /home/startup/openshift.local.clusterup/openshift.local.volumes/pods/c6177318-30b7-11e9-a791-b00cd12adb18/volumes/kubernetes.io~configmap/webconsole-config
# ls -la
합계 0
drwxrwsrwx. 4 root 1000120000 128  2월 15 14:35 .
drwxr-xr-x. 3 root root        31  2월 15 09:22 ..
drwxr-sr-x. 2 root 1000120000  36  2월 15 14:34 ..2019_02_15_00_22_27.301091537
drwxr-sr-x. 2 root 1000120000  36  2월 15 14:35 ..2019_02_15_05_35_01.192537530
lrwxrwxrwx. 1 root 1000120000  31  2월 15 14:35 ..data -> ..2019_02_15_05_35_01.192537530
lrwxrwxrwx. 1 root root        29  2월 15 09:22 webconsole-config.yaml -> ..data/webconsole-config.yaml

vi webconsole-config.yml
127.0.0.1 --> 192.168.29.106 으로 수정.
```



```
$ oc cluster up


...
" "sample-templates/mongodb" "sample-templates/mariadb" "sample-templates/mysql" "sample-templates/postgresql" "sample-templates/cakephp quickstart" "sample-templates/dancer quickstart" "sample-templates/jenkins pipeline ephemeral" "sample-templates/sample pipeline"
I0215 09:22:23.928148    3199 interface.go:41] Finished installing "sample-templates" "persistent-volumes" "openshift-web-console-operator" "centos-imagestreams" "openshift-image-registry" "openshift-router"
Login to server ...
Creating initial project "myproject" ...
Server Information ...
OpenShift server started.

The server is accessible via web console at:
    https://127.0.0.1:8443/console

You are logged in as:
    User:     developer
    Password: <any value>

To login as administrator:
    oc login -u system:admin

[startup@localhost ~]$  https://127.0.0.1:8443/console

```

https://startup:8443/console  로 접속.




## 레퍼런스 ##

http://snowdeer.github.io/openshift/2018/02/18/install-openshift-origin/

