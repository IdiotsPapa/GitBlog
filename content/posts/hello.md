---
title: "Hello, Git 블로그!"
date: 2025-07-16T22:00:00+09:00
draft: false
tags: ["Git", "블로그"]
categories: ["기술"]
---

이것은 Hugo + GitHub Pages로 만든 첫 번째 포스트입니다 🎉  
앞으로 개발 기록, 팁, 문서 등을 여기에 남길 예정입니다.

✅ 1. 프로젝트 목표
Hugo + GitHub Pages로 정적 블로그 생성
저장소: https://github.com/IdiotsPapa/GitBlog


🛠️ 2. 사용된 명령어 및 역할
명령어	역할
choco install hugo -confirm	Chocolatey로 Hugo 설치
hugo version	설치된 Hugo 버전 확인
hugo new site hugo-blog	새 Hugo 블로그 프로젝트 생성
cd hugo-blog	생성된 폴더로 이동
git init	Git 초기화
git remote add origin https://github.com/...	GitHub 원격 저장소 연결
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod	PaperMod 테마 추가
hugo new posts/hello.md	새 블로그 글 생성
hugo	정적 파일(public 폴더) 빌드
git checkout --orphan gh-pages	GitHub Pages용 빈 브랜치 생성
git rm -rf .	gh-pages 브랜치의 모든 파일 삭제
git add, git commit, git push	변경사항 커밋/푸시
.github/workflows/gh-pages.yml 작성	GitHub Actions 자동 배포 설정
git push origin main	Hugo 소스와 설정 푸시 (자동 배포 트리거)



📂 3. Hugo 프로젝트 구조
Hugo는 다음과 같은 기본 구조로 생성됩니다:

csharp
복사
편집
hugo-blog/
├── archetypes/         # 새 콘텐츠 템플릿
│   └── default.md
├── content/            # 실제 포스트들 위치
│   └── posts/
│       └── hello.md
├── layouts/            # 커스텀 레이아웃 (선택)
├── static/             # 정적 리소스 (이미지, JS 등)
├── themes/             # 테마 저장소 (여기선 PaperMod)
│   └── PaperMod/
├── public/             # Hugo 빌드시 생성되는 정적 HTML
├── config.toml (또는 hugo.toml)  # 설정파일
└── .github/
    └── workflows/
        └── gh-pages.yml   # 자동 배포 설정




 🔁 4. GitHub Pages 자동 배포 흐름
main 브랜치에 글/설정 푸시

GitHub Actions가 hugo로 빌드

public/ 내용을 gh-pages 브랜치에 푸시

gh-pages 브랜치가 GitHub Pages로 호스팅됨



🌐 5. 최종 결과 URL
항목	주소
블로그 메인	https://idiotspapa.github.io/GitBlog/
첫 글	https://idiotspapa.github.io/GitBlog/posts/hello/
테스트 글	https://idiotspapa.github.io/GitBlog/posts/test/

✅ 6. 다음 단계 추천
about.md, tags, categories 페이지 생성

이미지 업로드 및 코드 블록 활용

Google Analytics 연동

SEO 메타 설정 (favicon, og:image 등)



