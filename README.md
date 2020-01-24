# node.js - 쿠키와 인증

## 관련 사이트

https://developer.mozilla.org/ko/docs/Web/HTTP/Cookies

## 쿠키의 생성

res.writeHead(200, {
"Set-Cookie": ["yummy_cookie=choco", "tasty_cookie=strawberry"]
});

## 쿠키의 읽기

https://www.npmjs.com/package/cookie

npm install -s cookie

## Session cookies

위에서 생성된 쿠키는 세션 쿠키입니다

클라이언트가 종료되면 삭제(delete)될 것입니다, 이유는 Expires 혹은 Max-Age를 명시하지 않았기 때문입니다.

그러나 웹 브라우저는 세션 복구를 할 수 있으며, 이 기능은 브라우저가 결코 닫힌 적이 없던 것처럼 대부분의 세션 쿠키들을 영속적인 것으로 만듭니다.

## Permanent cookies

클라이언트가 닫힐 때 만료되는 대신에, 영속적인 쿠키는 명시된 날짜(Expires)에 만료되거나 혹은 명시한 기간(Max-Age) 이후에 만료됩니다.

Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;

Expires = 만료되다.(절대적인 것.)

Max-Age = 쿠기가 얼마동안 살 것인가.(현재시점을 기준으로 얼마동안 살아있을 것인가.)
