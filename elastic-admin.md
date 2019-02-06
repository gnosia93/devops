```
@ cluster health check
$ curl -X GET "localhost:9200/_cluster/health" | python -m json.tool



@ node monitoring 
$ curl -X GET "http://localhost:9200/_nodes/stats" | python -m json.tool | more

```

## 레퍼런스 ##

https://www.elastic.co/guide/en/elasticsearch/guide/current/_cluster_health.html
