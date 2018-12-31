## 설치 ##
```
echo "deb http://www.apache.org/dist/cassandra/debian 311x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
curl https://www.apache.org/dist/cassandra/KEYS | sudo apt-key add -
sudo apt-key adv --keyserver pool.sks-keyservers.net --recv-key A278B781FE4B2BDA
sudo apt-get update
sudo apt-get install cassandra
```

/etc/cassandra/cassandra.yml 파일에 설정한다. 

외부 테스트 툴로 부터 9042 port 로 접속이 되지 않는 경우 아래와 같이 설정한다. default 는 localhost 에서만 접근 가능하다. 

```
rpc_address: 0.0.0.0
broadcast_rpc_address: 1.2.3.4

```


