## php-session


```Session```이란? 서버측에 정보를 저장하는 슈퍼글로벌 변수다.


1) 시작
```
if (session_status() == PHP_SESSION_NONE) {
    session_start();
} 
```
Session ID값이 None인 경우 session 할당 

2) 종료
```
session_unset(); // $_SESSION 모든값 초기화
session_destroy(); // $_SESSION 해제 id값 만료
```
확실하게 안전하게 Session을 해제하기 위해서 ```session_unset```, ```session_destroy``` 두 함수를 이용하여 제거 합니다.  









Q) 백엔드를 개발하면서 SESSION에 대해서 고민을 해본적이 있나?
```
유저 A) $_sESSION['userid'] = 'test1';
유저 B) $_sESSION['userid'] = 'test2';
```
서버입장에서 SESSION의 같은 key값으로 어떻게 유저별로 다른 userid를 호출 할 수 있게 되는가?
PHP는 HTTP 요청별로 프로세스를 생성하는 특성을 가지고 있고, 새션이 실행될때마다 고유의 session id 값이 생성된다.










```
싱글패턴은 인스턴스가 오직 하나만 존재하도록 하는 객체지향 디자인패턴 중 하나의 방법
```

PHP는 HTTP 요청에 마다 별도의 프로세스가 생겨 싱글패턴이 의미가 거의 없어 싱글패턴으로 구현하느 것은
좋은 밥법이 아닐 수 있다
