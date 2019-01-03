## 개념 ##

mongodb는 여러개의 DB 로 구성되어 있으며, 컬렉션은 rdbms 의 테이블에 해당한다.

튜플은 document 이며, schema less 이다.

조인 개념이 없으며, document의 pk를 명시적으로 선언하지 않으면

mongodb 에서 생성해 준다. 


## 데이터베이스 생성 ##

mongodb 의 default 데이터베이스는 test 로, use 명령어를 이용하여 DB를 명시적으로 생성하지 않는 경우,

모든 컬렉션은 test DB 에 저장된다.

use 명령어를 이용하여 데이터베이스를 생성하더라도, 데이터를 입력하지 않으면 show dbs

결과에 생성된 DB 는 보이지 않는다 


```
> use mydb                                        # 데이터베이스 생성
> db                                              # 현재 선택된 DB 조회
> show dbs                                        # 데이터베이스 리스트 조회 
> db.movie.insert({"name":"tutorials point"})     # movie 컬렌션 입력
> show dbs                 
```

## 데이터베이스 삭제 ##
```
> use mydb                            # 삭제할 db 선택
> db.dropDatabase()                   # db 삭제
> show dbs
```

## 컬렉션(테이블) 생성 ##
```
> use test
> db.createCollection("myTable")                     # 컬렉션을 생성
> show collections
> db.tutorialspoint.insert({"name":"tutorial"})      # 컬렉션이 없더라도 insert 하는 경우 해당 컬렉션이 만들어 진다.  
> show collections
```

## 컬렉션 삭제 ##
```
> use test
> show collections
> db.myTable.drop()
> show collections
```


https://www.tutorialspoint.com/mongodb/index.htm





