##### PHP Composer

```PHP 라이브러리 의존성 관리 패키지 관리자```

사내에서는 composer 사용이 전무했으며, 라이브러리 코드를 직접 넣는 방법을 채택하고 있었다
위의 방법이 잘못된 방법은 아니다 지원이 종료됬거나 사용하는 php버전이 낮은 경우에는 어쩔 수 없이 직접 넣는 방법밖에는 없는 없다.
하지만 패키지 관리자를 통해서 라이브러리를 다운 받아 사용하는 것이 의존성, 업데이트 같은 문제가 충분히 발생 할 수 있기 때문에 Composer와 같은 패키지 관리자는 사용하는 것이
유지보수면에서 큰 장점이 있다고 생각해서 도입을 추진 했다.


분명 Python, Node에서 사용하는 패키기 관리자가 php에서도 있다고 생각했으며 찾아낸것이 composer 였다.
```Composer```는 ```pip```,  ```npm``` 와 비슷하다고 볼 수 있다.
composer는 ```composer.json``를 이용하여 라이브러리 버전관리와 autoload ... 설정 할 수 있는 파일이고
json 파일로 구성되어 직관적으로 사용하기 쉽다.

Python에서도  비슷한 ```requirement.txt```가 있지만  패키지만 다운로드 하는 단순한  기능만 있다.

PHP
```
composer install php-jwt
```

Python
```
 pip3 install requests 
```

Node.js
```
npm install axios
```


```
composer intsall composer.json
```












