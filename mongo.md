## 설치 ##

```
# add key
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
# add library repo to repo list
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
# update repos
sudo apt-get update
# install mongodb
sudo apt-get install -y mongodb-org
```

## 서비스 관리 ##

```
sudo service mongod start  # 기동
sudo service mongod restart  # 재기동
sudo service mongod stop  # 정지
sudo service mongod status   # 상태보기
```

## 서비스 등록 ##

위와 같이 설치 후 service 커맨드를 이용하여 mongod 를 기동 및 정지 할 수 있다. 

이와 관련하여 문제가 발생하는 경우 아래와 같은 방식으로 조치한다. 

/etc/systemd/system/mongodb.service 의 내용을 아래와 같이 만든다. 

```
[Unit]
Description=High-performance, schema-free document-oriented database
After=network.target

[Service]
User=mongodb
ExecStart=/usr/bin/mongod --quiet --config /etc/mongod.conf

[Install]
WantedBy=multi-user.target

```

아래 명령어 들을 이용하여 시작, 상태체크 및 서비스 등록한다. 

sudo systemctl start mongodb

sudo systemctl status mongodb

sudo systemctl enable mongodb


## Admin ##

### root 계정 생성 ###
mongo 클라이언트를 실행하여 admin DB 에 접속한 후, root 계정을 생성한다. 

```
startup@startup:/etc/systemd/system$ mongo
MongoDB shell version: 3.2.22
connecting to: test
> use admin
switched to db admin
> db.createUser ({user:'root', pwd:'root', roles:["root"]})
Successfully added user: { "user" : "root", "roles" : [ "root" ] }
> quit()

```

### DB 생성 및 DB 유저 새성 ###

```
$ mongo -u "root" -p "root" --authenticationDatabase "admin"


```



