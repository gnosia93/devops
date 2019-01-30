## 소프트웨어  ##

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

로그 파일에 보면 아래와 같은 라인을 찾을 수 있다. 
2019-01-30T16:13:39.222605Z 1 [Note] A temporary password is generated for root@localhost: PdiWo(kpw8oM


# jenkins 설치
> sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
> sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
> sudo yum install jenkins
> sudo vi /etc/sysconfig/jenkins

JENKINS_PORT=“8080”   --> 9090 으로 변경.

> sudo systemctl enable jenkins 
> sudo systemctl start jenkins
> sudo firewall-cmd --permanent --add-port=9090/tcp             -- 방화벽 
> sudo firewall-cmd --reload


# elasticsearch
# https://soulsearcher.github.io/blog/2018/02/12/elastic_on_centos/

> sudo vi /etc/yum.repo.d/elastic.repo

[elasticsearch-6.x]
name=Elasticsearch repository for 6.x packages
baseurl=https://artifacts.elastic.co/packages/6.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md

> sudo yum install elasticsearch -y
> sudo systemctl enable elasticsearch
> sudo systemctl start elasticsearch


# kibana
> sudo yum install kibana -y


# logstash
> sudo yum install logstash -y

```




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
