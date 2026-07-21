+++
date = '2026-07-21T13:25:00+09:00'
draft = false
title = 'FreshPeach — .NET 8 + Vue 개발 환경 검증'
tags = ['.NET 8', 'ASP.NET Core', 'Vue', 'TypeScript']
summary = 'ASP.NET Core API와 Vue 프론트엔드의 분리 구성을 확인한 초기 기술 검증'
period = '2026'
role = '기술 검증'
featured = false
order = 12
category = 'web'
+++

서비스를 만든 결과물이라기보다 **.NET 8 API와 Vue를 분리해 같이 쓰기 위한 초기 스캐폴드**입니다. 서로 다른 출처에서 개발 서버를 띄울 때 필요한 구조와 CORS를 확인했습니다.

## 확인한 것

백엔드: .NET 8 · ASP.NET Core Web API · Swagger · EF Core/PostgreSQL 자리 마련.  
프론트: Vue 3 · TypeScript · Vite · Pinia · Vue Router · ESLint / `vue-tsc`.

CORS는 `builder.Build()` 전에 서비스를 등록해야 한다는 점을 이 과정에서 다시 확인했습니다. 연결 문자열을 소스에 두는 문제는 남아 있어, 이어 개발한다면 Secret·환경변수로 분리해야 합니다.

## 아직 만들지 않은 것

도메인 API, 로그인, 사용자 CRUD, 실데이터 화면, 배포. Vue도 템플릿 수준입니다. **완성 서비스가 아니라 분리 구성·개발 환경 검증용 스캐폴드**입니다.
