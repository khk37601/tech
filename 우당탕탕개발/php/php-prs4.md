## PHP prs-4

#### autoload 표준

```
prs-0을 대체하는 표준이며, 네임스페이스를 파일 시스템 디렉토리에 대응함.
```

##### 적용기

```
사내 레거시 환경은 PHP5.3를 사용하며 Namespace, Composer사용이 전무한 상태였으며,
prs 0 ~ 4 표준을 새로운 서비스와 레거시 서비스에 부분적으로 적용 하기로 했다.
```

##### namespace 적용
```
namespace는 클래스의 톡립적인 환경이 구성해 충돌을 방지하고
소스코드에 덕지덕지 있는 include_once, require_once 소스코드를 줄이는 장점이 있다. 
```

##### 예시)

* src > lib > standard > Standard.php

```
<?php

class Standard
{
    public static function isBlank(string $text): bool 
    {
       // 로직
    } 
}
```

* src > main.php
```
<?php
  include_once $_SERVER['DOCUMENT_ROOT'] . '/src/lib/standard/Standard.php';
  Standard::isBlank($_POST['no']);
```


🙏 ```변경)```

* src > lib > standard > Standard.php

```
<?php
    namespace labs/src/lib/starndard;


    class Standard
    {
        public static function isBlank(string $text): bool 
        {
           // 로직
        } 
    }
```

* src > main.php
```
<?php
    use namespace labs/src/lib/starndard;

    Standard::isBlank($_POST['no']);
```


* 각 클래스별 독립성과 표준을 준수하면서 코드의 가용성 향상과 일관성을 유지하면 생산성의 증대를 기대 하게 됨.


##### autoload 적용

```
class <사내서비스>/경로/파일이름
```


* composer.json

```
 {
   "autoload": {
      "prs-4": {
          "labs//src//lib//Fn": "src/lib/Fn"
           ...
       }
   }
 }
```

* autoload 적용 명령어
```
composer dump-auto
```

##### 개발자가 직접 spl_autoload_register()사용 없이 네임스페이드를 파일과 맵핑시켜 획기적으로 클래스를 호출하도록 변경되었습니다.
