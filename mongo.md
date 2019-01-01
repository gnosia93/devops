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

sudo nano /etc/systemd/system/mongodb.service
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


sudo systemctl start mongodb

sudo systemctl status mongodb

sudo systemctl enable mongodb



