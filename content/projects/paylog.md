+++
date = '2026-07-21T13:23:00+09:00'
draft = false
title = 'PayLog — 결제 알림 기반 지출·정산 앱'
tags = ['Flutter', 'Dart', 'Android', 'Kotlin']
summary = 'Android 결제 알림을 거래로 변환하고 개인 지출과 그룹 정산을 관리하는 Flutter MVP'
period = '2026.05 — 06'
role = '개발'
featured = false
order = 8
category = 'mobile'
+++

카드 결제 알림을 거래로 바꾸고, 개인 지출·그룹 정산을 관리하는 Flutter 앱입니다.

- 작업 기간: 2026년 5월 27일 ~ 6월 11일
- 상태: Android 중심 기능성 MVP
- 핵심: Flutter ↔ Android 알림 네이티브 연동

## 화면 밖에서 시작되는 앱

가장 까다로웠던 것은 가계부 UI가 아니라, 앱이 꺼져 있을 때 도착한 결제 알림을 놓치지 않는 일이었습니다.

```text
NotificationListenerService
  ├─ 앱 실행 중 → EventChannel로 Flutter 전달
  └─ 앱 미실행 → SharedPreferences 큐 저장 → 다음 실행 시 변환
```

Kotlin 서비스와 Flutter는 MethodChannel·EventChannel로 연결하고, 알림 접근 권한 확인·설정 화면 이동을 제공합니다.

## 알림을 거래로 바꾸기

금액·가맹점·카드사를 추출하고, 승인 취소·거절 문구는 거래로 만들지 않습니다. 일정 시간 안 중복도 막습니다. 파서는 휴리스틱이라 모든 실제 알림을 안정 처리한다고 말할 수 없고, 광범위 실기기 검증도 아직입니다.

## 정산 범위

지출자와 결제자를 따로 두고 멤버별 채권·채무·송금 방향을 계산합니다. 현재는 단일 지출자·단일 결제자 기준이며, 한 거래를 여러 명에게 비율로 나누는 기능은 없습니다. 월별·카테고리별 집계와 멤버·그룹 관리(참조 중인 항목 삭제 방지)를 포함합니다.

데이터는 SharedPreferences에 두며, 규모가 커지면 로컬 DB로 옮겨야 합니다. 로그인·백업·동기화·iOS 자동 수집·정식 배포는 없습니다. **Flutter–Android 알림 연동의 핵심을 확인한 MVP**입니다.
