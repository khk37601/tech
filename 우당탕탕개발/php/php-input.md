## PHP input 


#### filter_input, filter_var, filter_input_array

```
 SQL 인젝션, 크로스사이트 스크립팅(XSS) 보안 문제 방지 뿐만 아니라 
 코드의 가독성이 향상되고 코드의 유지보수가 좋아짐
```

사례)
가능한 fiter_input, filter_var, filter_input_array로 변경하거나 새로운 로직 구성을 했습니다.

기존)
```

 if (strpos($email, '@') !== false) {
    ...
 }

 if(is_array($phone)) {

     checkBlank($phone[0],'전화번호를');
     
     checkBlank($phone[1],'전화번호를');
     
     checkBlank($phone[2],'전화번호를');
 }

 if (is_numeric($age)) {
     if ($age < 15 || $age > 99) {
         .....
     }
 }
```

🙏 ```변경```)
```
filter_input_array(INPUT_POST, [
    'phone' => [
        'filter' => FILTER_CALLBACK,            
        'options' => 'validate_phone_number'
    ],
    'age' => [
         'filter' => FILTER_VALIDATE_INT,
         'options' => ['min_range' => 15 , 'max_range' => 99]
    ],
    'email' => [
         'filter' => FILTER_VALIDATE_EMAIL
    ] 
]);
```
더보기 > [유효성 검사 패턴](https://www.php.net/manual/en/filter.constants.php#constant.filter-default)


장점) 
1. 코드의 가독성 향상
2. 안정성과 보안성을 증대 시킴

결국 코드는 작동만 하는것이 아니라 다른 개발자가 봐도 이해하기 쉽고 유지보수가 쉬워야한다.

