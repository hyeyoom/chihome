---
title: "Hugo 시작하기"
weight: 1
bookToc: true
---

# Hugo 시작하기

Hugo와 hugo-book 테마를 사용한 첫 번째 포스트입니다.

## Hugo란?

Hugo는 Go로 작성된 정적 사이트 생성기(Static Site Generator)입니다. 빠른 빌드 속도와 간단한 사용법이 특징입니다.

### 주요 특징

- **빠른 속도**: Go 언어로 작성되어 매우 빠른 빌드 속도
- **간편한 사용**: 복잡한 설정 없이 바로 시작 가능
- **다국어 지원**: 기본적으로 다국어 사이트 구축 지원
- **풍부한 테마**: 다양한 무료 테마 제공

## hugo-book 테마

이 사이트는 hugo-book 테마를 사용하고 있습니다. hugo-book은 문서 작성에 최적화된 깔끔한 디자인의 테마입니다.

### 주요 기능

- 깔끔하고 심플한 디자인
- 모바일 친화적
- 다크 모드 지원
- 검색 기능 내장
- 목차(ToC) 자동 생성

## 다국어 설정

이 사이트는 한국어와 영어를 지원합니다. 언어 전환은 상단 메뉴에서 가능합니다.

```toml
# hugo.toml
defaultContentLanguage = 'ko'

[languages]
  [languages.ko]
    languageName = '한국어'
    contentDir = 'content.ko'
    weight = 1

  [languages.en]
    languageName = 'English'
    contentDir = 'content.en'
    weight = 2
```

## 블로그 운영 가이드

블로그를 효과적으로 운영하기 위한 가이드입니다:

- [포스트 작성하기]({{< relref "guide/writing-posts" >}}) - 새 포스트 작성 방법과 Front Matter 설정
- [콘텐츠 구성하기]({{< relref "guide/organizing-content" >}}) - 카테고리, 태그, 메뉴 구성
- [SEO 최적화]({{< relref "guide/seo-optimization" >}}) - 검색 엔진 최적화 설정

## 다음 단계

- 테마 커스터마이징
- 배포 설정 (GitHub Pages, Netlify 등)
