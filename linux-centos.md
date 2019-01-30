## Admin ##

```
# putty 설정
https://stove99.tistory.com/172
https://stackoverflow.com/questions/20864224/putty-getting-server-refused-our-key-error/29292390

# sudoer 등록
https://sseungshin.tistory.com/82

# docker 설치
http://www.kwangsiklee.com/2017/07/centos%EC%97%90%EC%84%9C-docker-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0/

# mysql 설치
> wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
> sudo rpm -ivh mysql57-community-release-el7-11.noarch.rpm
> sudo yum install mysql-server
> sudo systemctl enable mysqld
> sudo systemctl start mysqld
> cat /var/log/mysqld.log            -- 설치시 발급되는 임시 비밀번호.
> mysql_secure_installation
```


2019-01-30T16:13:39.222605Z 1 [Note] A temporary password is generated for root@localhost: PdiWo(kpw8oM


## Nginx ##

```
$ sudo vi /etc/yum.repos.d/nginx.repo

[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1

$sudo yum install -y nginx
```
