## PHP Composer

```PHP 라이브러리 의존성 관리 패키지 관리자```

##### 도입)
```
사내에서는 composer 사용이 전무했으며, 라이브러리 코드를 직접 넣는 방법을 채택하고 있었다
위의 방법이 잘못된 방법은 아니다 지원이 종료됬거나 사용하는 php버전이 낮은 경우에는 어쩔 수 없이 직접 넣는 방법밖에는 없다.
하지만 패키지 관리자를 통해서 라이브러리를 다운 받아 사용하는 것이 의존성과 버전 관리를 위해서 Composer를 사용하는 것이
유지보수면에서 큰 장점이 있다고 생각해서 도입을 추진 했다.
```
PHP
```
composer install php-jwt
```
```Composer```는 ```pip```,  ```npm``` 와 비슷하다고 볼 수 있다.

composer는 ```composer.json```를 이용하여 라이브러리 버전관리와 autoload ... 설정 할 수 있는 파일이고 json 파일로 구성되어 직관적이여서 사용하기 쉽다.

```
{
 "require": {
    "monolog/monolog": "1.0.*",
    "firebase/php-jwt": "*"
 },
 "require-dev": {
     "mockery/mockery": "dev-master",
     "phpunit/phpunit" : "3.7.*",
     "codeception/aspect-mock": "*"
 },
 autoload: {
    "prs-4": {
        "lab//src//lib/": "src/lib"
         ....
     }
 }
}
```

개발서버)
```
composer update // 종속 항목 최신버전 업데이트 composer.lock 파일 업데이트 
composer install // composer.lock 기준으로 버전 설치 만약 composer.lock파일이 없으면 composer.json 설치 후 .lock 파일 생성
```

서비스서버)
```
composer update --no--dev
composer install --no--dev 
```





