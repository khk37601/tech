## php-trait

```
php를 사용하면 정말 신비한 키워드가 있다. 바로 trait
triat의 문법을 보고 있으면 신기함을 느꼈다
왜나면 Python, node, Java ... 등 다른 언어를 사용하면서 경험해 보지 못했던 문법이였다.
```

상속의 일반적인 방법

PHP:
```
namespace lab/src/test

class A extends B
{
  public function __construct()
  {
  }
}

```


Python:
```
 class B(A)
 {
   def __init__(self):
        super().__init__()
 }
```

Java:
```
class A extends B {
  public void A(){
     super();
  }

}
```

PHP > trait

```
trait B
{
}

class A
{
 use B;
}
```
위처럼 사용하면 B에있는 메소드를 사용 할 수 있게 된다.
class는 기본적으로 단일 상속으로 이루어져있지만 trait은 다중상속을 가능하게 해준다.




