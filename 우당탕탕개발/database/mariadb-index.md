### index

```index```는 책의 목차와 같은 역할과 같다고 할 수 있다

영어사전에서 ```select``` 단어를 찾아 본다고 가정해보자

 1. ```A``` 부터 ```select```가 나올때까지 처음부터 끝까지 조사.
 2. 목차에서 ```S```를 찾아서 ```select```를 조사.

우리는 본능적으로 두 번째 방법으로 찾는다 우리가 쓰는 database도 마찬가지이다 

table에서 index를 설정하면 해당 table에 관련된 index 테이블을 따로 구성해서 저장 한다
사용자가 where절에 index가 포함된 컬럼이 검색이 되면 index 테이블을 조회 해서 table의 내용을 검색 하는 원리 이다
이때 index는 ```btree```로 구성되어있다.

데이터가 update, insert, delete가 발생한다면 index 테이블도 변환된다
index의 테이블의 크기가 크다면 당연히 ```update, insert, delete``` 작업에 시간이 더 소요된다고 할 수 있다.








