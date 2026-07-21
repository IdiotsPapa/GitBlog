+++
date = '2026-07-21T13:25:00+09:00'
draft = false
title = 'FreshPeach — .NET 8 + Vue 개발 환경 실험'
tags = ['.NET 8', 'ASP.NET Core', 'Vue', 'TypeScript']
summary = 'ASP.NET Core API와 Vue 프론트엔드의 분리 구성을 확인한 초기 기술 실험'
+++

## 프로젝트 성격

ASP.NET Core Web API와 Vue 프론트엔드를 분리해 구성한 **초기 기술 실험(Spike)** 입니다.

완성된 서비스나 도메인 프로젝트가 아니라, .NET 8과 Vue를 함께 사용할 때 필요한 프로젝트 구조·CORS·데이터 접근 구성을 확인하는 단계입니다.

## 구성한 기술

### 백엔드

- .NET 8
- ASP.NET Core Web API
- Swagger
- Entity Framework Core 구조 초안
- PostgreSQL 공급자

### 프론트엔드

- Vue 3 / TypeScript
- Vite
- Pinia
- Vue Router
- ESLint / Oxlint / vue-tsc

## 확인한 구조

```text
Vue 개발 서버
   ↓ HTTP API
ASP.NET Core Web API
   ↓
EF Core / PostgreSQL 후보
```

백엔드와 프론트엔드를 별도 프로젝트로 관리하고, 개발 중에는 서로 다른 출처에서 실행하는 구성을 시도했습니다.

## 현재 구현 수준

- ASP.NET Core API 기본 구조
- 개발 환경 Swagger
- 최소 데이터 모델과 DbContext 초안
- Vue 라우터·상태 관리 기본 구성
- 개발 서버 간 CORS 정책 실험

도메인 API, 로그인, 사용자 CRUD, 실제 데이터 표시와 배포는 구현되지 않았습니다. Vue 화면 역시 템플릿 수준입니다.

## 초기 실험에서 확인한 문제

### 서비스 등록 순서

ASP.NET Core에서는 `builder.Build()` 전에 서비스 등록을 마쳐야 합니다. 초기 코드에서 CORS 등록 위치가 잘못된 문제를 확인했고, 애플리케이션 빌드 전 서비스 구성을 완료해야 한다는 점을 정리했습니다.

### 비밀정보 분리

데이터베이스 연결 문자열을 소스에 직접 두는 방식은 안전하지 않습니다. 환경변수·개발용 Secret Manager·배포 환경의 Secret 저장소로 분리해야 합니다.

### 프론트와 API 계약

백엔드 DTO와 Vue TypeScript 타입을 별도로 작성하면 변경 시 불일치가 생길 수 있습니다. API 명세 또는 코드 생성을 통해 계약을 일치시키는 방법을 추가로 검토할 필요가 있습니다.

## 기록하는 이유

포트폴리오에는 완성작만 있는 것이 아니라, 기술을 도입하기 전에 작은 범위로 검증한 기록도 필요하다고 생각합니다.

이 글은 결과를 과장하지 않고, **.NET 8 + Vue 조합을 탐색하며 발견한 구성·보안·계약 문제**를 남기기 위한 글입니다.
