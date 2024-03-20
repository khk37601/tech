## php-feature


##### 1) '' , "" 
```
'': 문자열 그대로 출력
"": 문자열내 변수 출력

$name = 'KJS';
echo 'hello $name'; // hello $name
echo "heelo $name"; // hello KJS
```

##### 2) 배열
```
PHP <= 5.3
1. $a = array(1, 2, 3);

PHP > 5.4
2. $a = [1, 2, 3]; // array(), [] 둘다 사용 가능.
```

##### 3)익명함수
```
php >= 5.3
$closure = function($x) {
    return $x + $x;
};
echo $closure(1); // 2
```

#### 4) type
```
PHP > 7
function randBox(int $a, int $b):int {
 return $a + $a;
}
```

##### 5) 병합 연산자
```
PHP < 7
1. if (isset($a)) {
      $a = '';
   }

PHP >= 7
2. $a = $a ?? ''
```




