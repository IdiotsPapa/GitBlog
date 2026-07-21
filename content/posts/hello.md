---
title: "Hugo + GitHub Pages로 개발 블로그 시작"
date: 2025-07-16T22:00:00+09:00
draft: false
tags: ["Hugo", "Git", "블로그"]
categories: ["기술"]
summary: "Hugo와 GitHub Pages, PaperMod 테마로 정적 블로그를 구성한 기록"
---

Hugo + GitHub Pages로 개인 개발 블로그를 만들었습니다.

## 구성

- 정적 사이트 생성: Hugo
- 테마: PaperMod
- 호스팅: GitHub Pages (`gh-pages`)
- 배포: `main` 푸시 시 GitHub Actions로 빌드·배포

## 콘텐츠 구조

```text
content/
├── posts/      # 일반 글
├── notes/      # 짧은 학습 기록
└── projects/   # 프로젝트 포트폴리오
```

섹션을 나누어 두면 메뉴와 URL이 단순해지고, 나중에 포트폴리오만 따로 관리하기 쉽습니다.

## 배포 흐름

1. `main`에 콘텐츠·설정 푸시  
2. Actions가 `hugo`로 `public/` 빌드  
3. `gh-pages` 브랜치에 게시  
4. `https://idiotspapa.github.io/GitBlog/` 에서 확인  

## 다음에 할 일

- 프로젝트 페이지를 실제 작업 기준으로 채우기  
- 초안(`draft: true`)과 공개 글을 구분하기  
- About에 기술 스택과 작업 방식 정리하기  
