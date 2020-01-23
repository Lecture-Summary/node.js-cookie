# node.js - 쿠키와 인증

## 관련 사이트

https://developer.mozilla.org/ko/docs/Web/HTTP/Cookies

## 쿠키의 생성

    res.writeHead(200, {
      "Set-Cookie": ["yummy_cookie=choco", "tasty_cookie=strawberry"]
    });
