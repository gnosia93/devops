## 인덱스 ##

일라스틱 서치의 인덱스의 RDBMS 의 데이터베이스와 같은 개념이다. 

```
# 모든 인덱스 리스트 조회
GET /_cat/indices?v

# 인덱스 삭제
DELETE /filebeat-*?pretty

{
  "acknowledged" : true
}

```

## 매핑 ##

일라스틱 서처의 매핑은 RDBMS 의 스키마와 같다.

```
# 매핑 조회
GET metricbeat-6.8.0-2019.05.29/_mapping
```




## 레퍼런스 ## 

https://bakyeono.net/post/2016-06-03-start-elasticsearch.html
