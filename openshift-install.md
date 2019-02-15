
## 설치 ##

최신버전 정보는 아래에서 확인할 수 있다. 

https://github.com/openshift/origin/releases

또한 github 에서는 소소 코드 또한 볼 수 있다 .. https://github.com/openshift/origin/tree/v3.11.0 


```
$ wget https://artifacts-openshift-release-3-11.svc.ci.openshift.org/zips/openshift-origin-server-v3.11.0-d0c29df-98-linux-64bit.tar.gz
$ tar xvfz openshift-origin-server-v3.11.0-d0c29df-98-linux-64bit.tar.gz
$ cd openshift-origin-server-v3.11.0-d0c29df-98-linux-64bit
$ sudo cp openshift oc kubectl /usr/local/bin
$ sudo oc cluster up
$ sudo firewall-cmd --add-port=8443/tcp --permanent
$ sudo firewall-cmd --reload
```


## 에러1 ##
```
[startup@localhost ~]$ sudo oc cluster up
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

## 에러2 ##
```


```

```
$ sudo usermod -a -G docker startup

```

## 레퍼런스 ##

http://snowdeer.github.io/openshift/2018/02/18/install-openshift-origin/

