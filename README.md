# Hugo 씨앗 템플릿

특정 테마에 의존하지 않는, 아주 단순한 Hugo 정적 사이트 템플릿입니다.
글쓰기·블로그 등 기본적인 사이트 하나를 빠르게 시작할 수 있도록
필요한 최소한의 구조만 담고 있습니다. 개발 지식이 없어도 아래 안내를
따라 내용/디자인을 바꿀 수 있습니다.

## 준비물

- [Hugo (extended 버전)](https://gohugo.io/installation/) 설치
  - macOS: `brew install hugo`
  - 설치 확인: `hugo version`

## 로컬에서 미리보기

프로젝트 폴더에서 아래 명령을 실행하세요.

```
hugo server -D
```

터미널에 나오는 주소(보통 `http://localhost:1313`)를 브라우저로 열면
현재 사이트를 미리 볼 수 있습니다. `-D`는 초안(draft) 글도 함께
보여주는 옵션입니다. 파일을 저장하면 화면이 자동으로 새로고침됩니다.
종료하려면 터미널에서 `Ctrl + C`를 누르세요.

## 새 글 추가하기

이 사이트는 한국어(ko)/영어(en) 두 언어를 지원합니다. 글 파일 이름
끝에 언어 코드를 붙여서 구분합니다.

- 한국어 글: `content/blog/글이름/index.ko.md`
- 영어 글: `content/blog/글이름/index.en.md`

가장 쉬운 방법은 기존 예시 글 폴더를 복사해서 이름과 내용만 바꾸는
것입니다.

```
content/blog/lorem-ipsum/index.ko.md   ← 이 파일을 참고/복사
```

또는 Hugo 명령으로 새 글의 뼈대를 만들 수도 있습니다.

```
hugo new blog/새글이름/index.ko.md
```

글 파일 맨 위에는 아래처럼 정보를 적는 부분(프론트매터)이 있습니다.

```
---
title: "글 제목"
author: 작성자 이름
date: 2026-08-16T12:00:00
brief: 목록에 보여줄 한 줄 요약
tags:
  - 태그1
  - 태그2
---

여기부터 본문을 마크다운으로 작성합니다.
```

그 아래에는 일반 마크다운(제목 `#`, 목록 `-`, 링크 `[텍스트](주소)` 등)으로
본문을 작성하면 됩니다. `draft: true`를 추가하면 실제 배포 시에는
보이지 않고 `hugo server -D`로 미리보기할 때만 보입니다.

## 새 페이지 추가하기 (About 같은 페이지)

`content/about/index.md`처럼 `content/` 아래 폴더를 새로 만들고
`index.md`를 추가하면 새 페이지가 됩니다. 메뉴에 표시하려면
`config.yml`의 `menu.primary` 항목에 추가하세요.

```yaml
menu:
  primary:
    - name: 새페이지이름
      url: /새페이지경로
      weight: 4
```

## 사이트 제목 / 메뉴 / 색상 바꾸기

- **사이트 이름, 메뉴**: `config.yml` 파일에서 `title`, `params.sitename`,
  `menu.primary` 항목을 수정하세요.
- **색상/폰트 등 디자인**: `static/css/custom.css` 파일을 여세요. 안에
  바꿀 수 있는 항목들이 한국어 설명과 함께 주석으로 정리되어 있습니다.
  원하는 줄의 주석(`/* */`)을 풀고 값을 바꾼 뒤 저장하면 됩니다.
  `assets/css/site.css`는 기본 레이아웃을 담당하는 파일이라 직접
  수정할 필요는 없습니다.

## 배포하기

이 저장소에는 GitHub Pages로 자동 배포하는 워크플로우가 이미
포함되어 있습니다 (`.github/workflows/hugo.yml`). GitHub 저장소를
만들고 `master` 브랜치에 push하면 자동으로 빌드되어 배포됩니다.

현재 이 프로젝트 폴더는 아직 git 저장소로 초기화되어 있지 않습니다.
GitHub에 올리려면 먼저 `git init` 후 원격 저장소를 연결하는 과정이
필요합니다.

## 폴더 구조 한눈에 보기

```
content/        실제 글/페이지 내용 (여기를 가장 많이 건드리게 됩니다)
static/css/     색상 등 디자인 설정 (custom.css)
static/js/      직접 추가할 스크립트가 있다면 여기에 (custom.js)
layouts/        페이지가 어떻게 그려질지 정하는 템플릿 (평소엔 건드릴 필요 없음)
assets/css/     기본 레이아웃 스타일 (건드리지 않는 것을 권장)
config.yml      사이트 전체 설정 (제목, 메뉴, 언어 등)
```
