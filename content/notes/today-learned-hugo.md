+++
date = '2025-07-17T00:39:49+09:00'
draft = false
title = 'Hugo에서 콘텐츠를 구분하는 방법'
+++

Hugo는 `content` 아래의 디렉터리를 기준으로 섹션을 구분한다.

```text
content/
├── posts/       # 일반 글
├── notes/       # 짧은 학습 기록
└── projects/    # 프로젝트 포트폴리오
```

각 Markdown 파일의 front matter에는 제목·작성일·공개 여부를 넣는다.

```toml
+++
title = "글 제목"
date = "2025-07-17T00:00:00+09:00"
draft = false
+++
```

작업 중인 글은 `draft = true`로 두면 일반 빌드에서 제외된다. 로컬에서 초안을 함께 확인할 때만 아래처럼 실행한다.

```powershell
hugo server -D
```

프로젝트 목록처럼 섹션 자체에 설명이 필요하면 `_index.md`를 사용한다. 개별 글을 늘리기 전에 섹션의 역할을 먼저 정해 두면 메뉴와 URL 구조가 단순해진다.
