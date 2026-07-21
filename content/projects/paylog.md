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

## 화면 밖에서 시작되는 앱

PayLog는 카드 결제 알림을 거래 내역으로 바꾸고, 개인 지출과 그룹 정산을 관리하기 위해 만든 Flutter 앱입니다.

- 작업 기간: 2026년 5월 27일 ~ 6월 11일
- 상태: Android 중심의 기능성 MVP
- 핵심: Flutter 앱과 Android 시스템 알림의 네이티브 연동

이 프로젝트에서 가장 까다로웠던 부분은 가계부 화면이 아니었습니다. 사용자가 앱을 보고 있지 않을 때 도착한 결제 알림을 놓치지 않는 일이었습니다.

## Flutter만으로 끝낼 수 없었던 이유

Android의 `NotificationListenerService`는 앱이 종료된 상태에서도 알림을 받을 수 있지만, 그 순간 Flutter 쪽이 실행 중이라는 보장은 없습니다. 처음부터 이벤트를 Flutter로 넘기는 것만 생각하면 앱이 꺼진 동안의 결제를 잃게 됩니다.

그래서 실행 상태에 따라 경로를 나눴습니다.

```text
Android NotificationListenerService
  ├─ 앱 실행 중: EventChannel로 Flutter에 전달
  └─ 앱 미실행: 네이티브 SharedPreferences 큐에 저장
                     ↓
                다음 앱 실행 시 읽고 거래로 변환
```

Flutter와 Android 네이티브의 생명주기가 다르다는 점을 전제로, 실시간 전달과 임시 저장을 분리했습니다. Kotlin 서비스와 Flutter는 MethodChannel·EventChannel로 연결했고, 앱에서는 알림 접근 권한 상태를 확인하거나 Android 설정 화면으로 이동할 수 있게 했습니다.

## 알림 한 줄을 거래로 바꾸기

알림에서 금액·가맹점·카드사를 추출하고, 승인 취소와 결제 거절 문구는 거래로 만들지 않도록 했습니다. 같은 알림이 반복해서 들어오는 경우에는 일정 시간 안의 중복 거래를 막았습니다.

문제는 카드사마다 문장 형식이 다르고 언제든 바뀔 수 있다는 것입니다. 현재 파서는 휴리스틱에 기대고 있어 모든 실제 알림을 안정적으로 처리한다고 말할 수 없습니다. 폭넓은 실기기 검증도 아직 하지 못했습니다.

## 정산은 어디까지 구현했나

거래에는 지출자와 실제 결제자를 따로 기록합니다. 이를 바탕으로 멤버별 채권·채무를 계산한 다음, 채권자와 채무자의 잔액을 비교해 필요한 송금 방향을 만듭니다.

현재 기준은 단일 지출자·단일 결제자입니다. 한 거래를 여러 명에게 균등 또는 비율로 나누는 기능까지 구현한 것은 아닙니다.

홈·정산·가계부·설정의 네 탭에서 거래를 직접 추가하고, 개인 또는 그룹 거래를 구분할 수 있습니다. 월별 거래와 총지출, 받을 돈을 표시하고 월별·카테고리별 소비도 집계합니다. 멤버와 그룹을 관리하되 기존 거래가 참조하는 항목은 삭제하지 못하게 막아 데이터가 끊어지지 않도록 했습니다.

## 지금의 기술 구성

앱은 Flutter와 Dart로 만들었고 Provider·ChangeNotifier로 상태를 관리합니다. Android 연동은 Kotlin, NotificationListenerService, MethodChannel, EventChannel을 사용했습니다. 현재 데이터와 미처리 알림 큐는 SharedPreferences에 저장합니다.

데이터가 많아지면 SharedPreferences 대신 로컬 DB로 옮겨야 합니다. 거래 수정·삭제 UI도 더 다듬어야 하며, 로그인·백업·동기화는 없습니다. 결제 알림 자동 수집은 Android만 지원하고 정식 배포도 아직 하지 않았습니다.

PayLog는 완성된 서비스가 아니라, Flutter 앱과 Android 네이티브 알림을 연결해 핵심 동작을 확인한 MVP입니다.
