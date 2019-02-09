## 방화벽 오픈 및 bind 설정 ##

firewall-cmd 명령어를 이용하여 9200 번 tcp 포트를 오픈하고, elasticsearch.yml 파일에 network.host 설정값을 0.0.0.0 으로 설정한다. 

```
$ sudo firewall-cmd --permanent --add-port=9200/tcp
success

$ cd /etc/elasticsearch

$ vi elasticsearch.yml
network.host: 0.0.0.0   추가.

$ curl -X GET "http://localhost:9200"
{
  "name" : "XYMCwzR",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "yS0MC1FRTHysTTP_Jv1HAQ",
  "version" : {
    "number" : "6.6.0",
    "build_flavor" : "default",
    "build_type" : "rpm",
    "build_hash" : "a9861f4",
    "build_date" : "2019-01-24T11:27:09.439740Z",
    "build_snapshot" : false,
    "lucene_version" : "7.6.0",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}
[root@localhost elasticsearch]#

```


## 레퍼런스 ##

https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-elastic-stack-on-centos-7


https://www.edureka.co/blog/elk-stack-tutorial/

https://logz.io/blog/elasticsearch-cluster-tutorial/
