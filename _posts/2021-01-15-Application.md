---
layout: post
title: 개발자 도구 - Application
date: 2021-01-15
tags: [기타]
---

## Application

💡 Application 패널의 기능

- 현재 로딩된 웹 페이지에서 사용된 리소스를 열람할 수 있는 패널
  (리소스 : 이미지, 스크립트, 데이터)
- 웹 SQL 데이터베이스, 로컬 및 세션 스토리지, 쿠키, 어플리케이션 캐시, 이미지, 폰트, 스타일시트를 포함한 로딩된 모든 리소스를 검사
- 로그인과 관련해서 유저정보에 대한 부분에도 많은 부분을 차지하기 때문에 꼭 알아두어야 할 패널

💡 Local Storage, Session Storage, Cookie 차이점

- Local Storage
  : 브라우저의 저장소로 사용자가 데이터를 지우지 않는 이상 브라우저에 계속 남아있다.
  : key-value 페어의 객체 형태로 데이터 저장
- Session Storage
  : 현재 떠 있는 탭이나 브라우저 내에서 유지되며 탭이나 브라우저를 종료하면 데이터는 사라진다.
- Cookie
  : key-value 페어의 문자열 형태로 데이터 저장
  : 시간제한이 설정되어있는 데이터 저장소
  : 프론트-백 통신과 관련이 있어 용량이 작을 수 밖에 없다.

💡 Local Storage, Session Storage, Cookie 사용 예시 - 어떤 데이터를 어디에 저장하면 좋을까?

- Local Storage
  : 지속적으로 필요한 데이터를 저장 ex) ID저장 등
- Session Storage
  : 잠깐동안 필요한 데이터를 저장 ex) 보안이 중요한 정보(은행사이트) 등
- Cookie
  : 빠른 처리가 필요한 임시 데이터 ex) 광고 팝업 등

💡 특정 데이터를 저장하고 가져오는 방법

- Local Storage
  저장 : localStorage.setItem("key","value")
  조회 : localStorage.getItem("key")
  삭제 : localStorage.removeItem("key")
  전체 삭제: localStorage.clear()

- Session Storage
  저장 : sessionStorage.setItem("key", "value")
  조회 : sessionStorage.getItem("key")
