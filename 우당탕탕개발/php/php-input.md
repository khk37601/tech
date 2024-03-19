## PHP input 


#### filter_input

```
 SQL 인젝션, 크로스사이트 스크립팅(XSS) 보안 문제 방지 뿐만 아니라 
 코드의 가독성이 향상되고 코드의 유지보수가 좋아짐
```

기존)

```
<?php
    if (strpos($email, '@') !== false);

```

변경)
```
<?php
    filter_input(INPUT_POST, 'email', FILTER_VALIDATE_EMAIL);
    
```



