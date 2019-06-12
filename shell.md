## AWK ##

NR 은 Number Of Record 로 header 를 제거하기 위해 NR > 1 사용함. 

```
$docker ps -a | awk 'NR > 1 { print "docker rm " $1 }'

docker rm 700dd8a677fd
docker rm 3cd231425f52
docker rm dc2670d4d7b5
docker rm abf23819bbad
docker rm e928587860d5
docker rm c670488c411d
docker rm 42e53d72cc13
docker rm 6271658d5b52
docker rm 652d4abdeb9b
docker rm dd6084cb7773
docker rm d434669240de
docker rm 06883f91badb
docker rm d1c793065349
```

### while 루프를 이용한 docker container 죽이기. ###
```
docker ps -a | awk 'NR > 1 { print $1 }' | while read contid
do
   docker stop $contid
   docker rm $contid
done
```
