---
layout: post
title: RESTful API
date: 2021-02-18
tags: [REST]
excerpt: RESTful API
---

# RESTful API

### 💡 REST 특징을 지키면서 API를 제공한다는 의미 !

---

REST(Representational State Transfer) 란?</br>
웹에 존재하는 모든 자원(ex 이미지,동영상 데이터)에 고유한 URI를 부여하여 자원에 대한 주소를 지정하는 방법론 또는 규칙으로 오늘날 가장 널리 사용되고 있다.

#### 1. 기본 배경 지식

- URI(Uniform Resource Identifier)
  - 해당 사이트의 특정 자원의 위치를 나타내는 유일한 주소
  - `/login`, `/news` 등
- HTTP Method
  - HTTP request가 의도하는 action을 정의한 것
  - `GET`,`POST` 등
- Payload
  - HTTP request에서 server로 보내지는 데이터 (body)

#### 2. Representational State Transfer란?

- 웹상에서 사용되는 여러 리소스를 HTTP URI로 표현하고 그 리소스에 대한 행위를 HTTP Method로 정의하는 방식  
  ➡️ 리소스(HTTP URI로 정의된)를 어떻게 한다(HTTP Method + Payload)를 구조적으로 깔끔하게 표현

#### 3. REST의 특징

1. Uniform(유니폼 인터페이스)

- 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍쳐 스타일이다.

2. Stateless(무상태성)

- 작업을 위한 상채정보를 따로 저장하고 관리하지않는다. 세션 정보나 쿠키정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만을 단순히 처리만 해주면 되기 때문에 구현이 쉽고 단순해진다.

3. 캐시 처리 가능(Cacheable)

- HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라 그대로 활용 가능하다.

4. Self-doescriptiveness(자체 표현 구조)

- REST API 메세지만 보고도 그 요청이 어떤 행위를 하는지 알 수 있다.

5. Client - Server 구조

- 클라이언트는 유저와 관련된 처리, 서버는 REST API를 제공함으로써 각각의 역할이 확실히 구분되고, 개발해야 할 내용이 명확해지고, 서로간의 의존성이 줄어든다.

6. 계층화(Layered System)

- 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있다. 그리고 프록시, 게이트웨이 등의 네트워크 기반의 중간매체를 사용할 수 있다.

#### RESTful API 설계 규칙

- URI 정보는 명확하게 표현해야 한다
- 리소스는 명사를 사용한다.
  ex) GET/user/1 → GET/users/1

- 리소스에 대한 행위를 HTTP Method(GET,POST,PUT,DELETE)로 표현한다.
  - URI에 HTTP Method가 포함되서는 안된다.
    ex) GET delete/user/1 → DELETE /users/1
  - 동사가 표함되서는 안된다.
    ex) GET /user/show/1 → GET /users/1
- 리소스 사이에 연관 관계가 있는 경우
  - /리소스/고유ID/관계 있는 리소스
    ex) GET /users/{user_id}/profile
- URI는 / 구분자를 사용하여 자원의 계층 관계를 나타내는데 사용한다.

  - ex) GET users/portfolios

- URI 마지막 문자로 /를 포함하지 않는다.
- 불가피하게 URI가 길어지는 경우 -을 사용하여 가독성을 높인다.
- \_는 사용하지 않는다.
- URI 경로에는 대문자 사용을 피하도록 규정하고 있다.
- 파일의 경우 payload의 포맷을 나타내기 위한 파일 확장자를 URI에 포함시키지 않는다.

#### RESTful 하지 못한 API 설계 예시

```
<나쁜 예시>                        <좋은 예시>

http://호스트/detail_page     => http://호스트/product
http://호스트/main_page       => http://호스트/products
http://호스트/find/product    => http://호스트/product
http://호스트/add/product     => http://호스트/product
http://호스트/product_reviews => http://호스트/product/1/reviews
http://호스트/product_filter  => http://호스트/product?name="abc"
```
