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

##### 6) heredoc
```
$table = <<<HTML
<table>
   <tr><td>$test</td></tr>
</table>
HTML; // 긴 문자열, html 표현에 편리한 기능
```

##### 7) array_filter
```
$a = [1, 2, 3, 4, 5];

$tmp = [];
foreach ($a as $_) {
    if ($_ % 2 == 0) {
        $tmpp[] = $_; 
    }
}

$abc = array_values(array_filter($a, functiuon ($_) {
    return $_ % 2 == 0;
}));

```



