```easyorder.wangpack.co.kr```
해당 서비스에서 로그인 인증 방법을 JWT(json web token)로 구현 하기로 정했습니다.


📌 JWT를 이용하여 로그인 인증을 고려한 이유는 세 가지 였습니다.

```
 1. 소규모의 회사에서 빠르게 서비스를 구현 하기에 비교적 구현이 쉬워서
 2. 서버의 부하를 최소화 하기 위해서
 3. 확장성이 뛰어나서(다른 서비스에도 사용이 가능 한점)
```
👀 JWT 는 과연 무엇일까?

```
jwt는 json web token 입니다.   
  json 객체를 이용하여 정보를 base64-url-Encode(링크) 인코딩하여 직렬화한 web token 입니다.

jwt의 구조
  {헤더(header)}.{내용(payload)}.{서명(signature)}
  구조로 이루어져 있습니다.
  (이때 jwt의 특징을 보면서 payload에 정보가 많으면 token의 길이가 길어져 결국 부하가 생기지 않을까 하는 생각이 꿈틀(🐍) 했다.)

  header:
     {
       'alg': 'HS256',
       'typ': 'jwt'
     }

 payload:
     {
        'iss': '토큰 발급자'
        'name': '김재석',
        'phone': '01046296852',
        'exp': '11111111111',
     }

 signature:
     HMASCHA256(
        base64UrlEncode(heder) + '.' +
        base64UrlEncode(payload),
        secret_key(사용자 지정, 복잡하고 유추하기 어려운 문자열을 구성하는 것을 추천)
     )

위의 정보를 토대로 jwt토큰 생성하게 됩니다.
```

🎉실제 적용한 사례
  ```
                     로그인                   Post v1/login 
    client <----------------------> web <----------------------> server
             sessionstorage 저장              jwt 발행 (유효기간 10분)    

                   jwt 전송                   jwt 유효기간 확인       
           <----------------------->     <----------------------->
                 서비스 접근                        인가
  ```

<span>
  <img src="https://github.com/khk37601/tech/blob/main/%EC%9A%B0%EB%8B%B9%ED%83%95%ED%83%95%EA%B0%9C%EB%B0%9C%20%EC%A0%81%EC%9A%A9%EA%B8%B0/web/%EC%9D%B4%EB%AF%B8%EC%A7%80/jwt%20%EB%A1%9C%EA%B7%B8%EC%9D%B8/%EC%95%84%EC%9D%B4%EB%94%94%EC%9E%85%EB%A0%A5.png" width="150">
</span>
<span>
  <img src="https://github.com/khk37601/tech/blob/main/%EC%9A%B0%EB%8B%B9%ED%83%95%ED%83%95%EA%B0%9C%EB%B0%9C%20%EC%A0%81%EC%9A%A9%EA%B8%B0/web/%EC%9D%B4%EB%AF%B8%EC%A7%80/jwt%20%EB%A1%9C%EA%B7%B8%EC%9D%B8/%ED%8C%A8%EC%8A%A4%EC%9B%8C%EB%93%9C%EC%9E%85%EB%A0%A5.png" width="150">
</span>

code:
  ```
 import time
 import jwt
 import hashlib

 from typing import Dict

 def get_jwt(data: Dict[str, str]) -> str:
     ten_minute = 60 * 10
     with EnvironmentManager as config:
         data['secret_key'] = hashlib.sha256((list(data.values())[0] + config.get('JWT_SALT')).encode()).hexdigest()
         data['exp'] = int(time.time()) + ten_minute
         token: Dict[str, str] = jwt.encode(
             data,
             config.get('JWT_KEY'),
             algorithm='HS256'
         )
      return token
  ```
 서버와 웹이 restapi를 통해 jwt 전자서명 발행 및 검증의 프로세스를 구현하여 고객들이 서비스를 이용하도록 구현 했습니다.    

🎊정리
  ```
   앞선 내용처럼 구현도 간단하고 서버의 부하도 줄이며 확장성도 뛰어난 장점이 있지만 단점이 존재 합니다
   JWT는 비교적 보안에 취약한 단점을 존재 합니다.

   1. 복호화가 쉽다
       base64기반으로 암호화 했기때문에 복호화가 비교적 간단하게 되는데 이때 payload의 내용이 노출되게 됩니다.
       그래서 payload에는 민감한 데이터를 담는 것은 추천 하지 않습니다.
       그래도 민감한 데이터를 담아야하는 상황이 생긴다면 payload 내용을 양방향 암호화하여 저장하는 것을 추천 합니다.
       (결국 서버의 부담이 생깁니다.)
   2. 탈취가 된 경우 서버에서 해당 토큰을 강제로 기간을 만료 시키는 것이 어렵다.
       탈취한 jwt는 서버에서는 유효한 토큰이기 때문에 서버에 접근이 가능해집니다
       이러한 문제를 해결하기 위해서는 
          A. jwt의 유효기간을 짧게 설정하여 피해를 최소화 한다.
          B. 탈취된 token의 블랙리스트를 만들어 접근을 막는다.
          C. refresh token를 이용하여 강제적으로 jwt(access token)을 재발행 한다(oauth 2.0에서 사용)   
  ```

🔬생길만한 의문점?
```
 jwt를 왜 cookie가 아닌 sessionstorage에 저장 했는가?
  >> 
```
