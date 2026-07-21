+++
date = '2025-07-17T00:39:49+09:00'
draft = false
title = 'Hugo에서 콘텐츠를 구분하는 방법'
+++

Hugo를 설정하면서 콘텐츠를 나누는 방법을 정리했다. `content` 아래의 디렉터리가 각 섹션이 된다.

```text
content/
├── posts/       # 일반 글
├── notes/       # 짧은 학습 기록
└── projects/    # 프로젝트 포트폴리오
```

각 Markdown 파일의 front matter에는 제목, 작성일, 공개 여부를 넣었다.

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

프로젝트 목록처럼 섹션 자체에 설명이 필요할 때는 `_index.md`를 사용한다. 섹션의 역할을 먼저 정해 두니 메뉴와 URL 구조를 단순하게 유지하기 쉬웠다.
