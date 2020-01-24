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

## Secure 과 Http Only Cookie

Secure 쿠키는 HTTPS 프로토콜 상에서 암호화된(encrypted) 요청일 경우에만 전송됩니다.

하지만 Secure일지라도 민감한 정보는 절대 쿠키에 저장되면 안됩니다, 본질적으로 안전하지 않고 이 플래그가 당신에게 실질적인 보안(real protection)를 제공하지 않기 때문입니다.

크롬52 혹은 파이어폭스52로 시작한다면, 안전하지 않은 사이트(http:) 는 쿠키에 Secure 설정을 지시할 수 없습니다.

Cross-site 스크립팅 (XSS) 공격을 방지하기 위해, HttpOnly쿠키는 JavaScript의 Document.cookie API에 접근할 수 없습니다.

그들은 서버에게 전송되기만 합니다.

예를 들어, 서버 쪽에서 지속되고 있는 세션의 쿠키는 JavaScript를 사용할 필요성이 없기 때문에 HttpOnly플래그가 설정될 것이다.

    Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure; HttpOnly

## 쿠키의 스코프

Domain 그리고 Path 디렉티브는 쿠키의 스코프를 정의합니다/

어떤 URL을 쿠키가 보내야 하는지.

Domain은 쿠키가 전송되게 될 호스트들을 명시합니다.

만약 명시되지 않는다면, (서브 도메인은 포함되지 않는) 현재 문서 위치의 호스트 일부를 기본값으로 합니다.

도메인이 명시되면, 서브도메인들은 항상 포함됩니다.

만약 Domain=mozilla.org이 설정되면, 쿠키들은 developer.mozilla.org와 같은 서브도메인 상에 포함되게 됩니다.

Path는 Cookie 헤더를 전송하기 위하여 요청되는 URL 내에 반드시 존재해야 하는 URL 경로입니다. %x2F ("/") 문자는 디렉티브 구분자로 해석되며 서브 디렉토리들과 잘 매치될 것입니다.

만약 Path=/docs이 설정되면, 다음의 경로들은 모두 매치될 것입니다:

/docs
/docs/Web/
/docs/Web/HTTP

    "Path=Path; Path=/cookie",
    "Domain=Domain; Domain=o2.org"
