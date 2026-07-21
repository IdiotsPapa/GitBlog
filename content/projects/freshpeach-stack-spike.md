+++
date = '2026-07-21T13:25:00+09:00'
draft = false
title = 'FreshPeach — .NET 8 + Vue 개발 환경 실험'
tags = ['.NET 8', 'ASP.NET Core', 'Vue', 'TypeScript']
summary = 'ASP.NET Core API와 Vue 프론트엔드의 분리 구성을 확인한 초기 기술 실험'
period = '2026'
role = '기술 실험'
featured = false
order = 12
category = 'web'
+++

FreshPeach는 서비스를 만들었다기보다 **.NET 8과 Vue를 같이 쓰기 위한 초기 스캐폴드**에 가깝습니다. ASP.NET Core Web API와 Vue 프론트엔드를 별도 프로젝트로 두고, 개발 중 서로 다른 출처에서 실행할 때 필요한 구조와 CORS 설정을 확인했습니다.

백엔드는 .NET 8, ASP.NET Core Web API, Swagger를 기준으로 잡았습니다. Entity Framework Core 구조와 최소 데이터 모델, `DbContext`는 초안만 만들었고 PostgreSQL 공급자를 붙일 자리를 마련했습니다. 프론트엔드는 Vue 3, TypeScript, Vite에 Pinia와 Vue Router를 구성했고 ESLint, Oxlint, `vue-tsc`를 사용했습니다.

## 스캐폴드를 만들며 확인한 것

ASP.NET Core API의 기본 골격과 개발 환경 Swagger, Vue 라우터와 상태 관리의 기본 구성까지 만들었습니다. 두 개발 서버 사이의 CORS 정책도 시험했습니다.

처음에는 CORS 서비스를 등록하는 위치가 잘못돼 있었습니다. ASP.NET Core에서는 `builder.Build()`를 호출하기 전에 서비스 등록을 끝내야 한다는 기본적인 순서를 이 과정에서 다시 확인했습니다.

데이터베이스 연결 문자열을 소스에 직접 두는 문제도 남아 있습니다. 실제로 이어서 개발한다면 환경변수, 개발용 Secret Manager, 배포 환경의 Secret 저장소로 분리해야 합니다.

프론트와 API의 계약을 어떻게 맞출지도 아직 정하지 못했습니다. 백엔드 DTO와 Vue의 TypeScript 타입을 각각 관리하면 변경할 때 어긋날 수 있어, API 명세나 코드 생성 방식은 추가로 검토할 항목입니다.

## 아직 만들지 않은 것

도메인 API, 로그인, 사용자 CRUD, 실제 데이터 표시와 배포는 구현하지 않았습니다. Vue 화면도 템플릿 수준입니다. 따라서 이 저장소를 완성된 서비스나 도메인 프로젝트로 소개하기는 어렵습니다.

남은 결과는 **ASP.NET Core API와 Vue 프론트엔드를 분리한 초기 스캐폴드**, 그리고 그 과정에서 확인한 구성·보안·계약 문제입니다.
