---
title: "포스트 작성하기"
weight: 2
bookToc: true
---

# 포스트 작성하기

Hugo에서 새로운 포스트를 작성하는 방법을 알아봅니다.

## 새 포스트 생성

Hugo CLI를 사용하여 새 포스트를 생성할 수 있습니다:

```bash
# 한국어 포스트 생성
hugo new content.ko/docs/my-first-post.md

# 영어 포스트 생성
hugo new content.en/docs/my-first-post.md
```

## Front Matter 설정

각 포스트의 상단에는 메타데이터를 정의하는 Front Matter가 있습니다.

### 기본 설정

```yaml
---
title: "포스트 제목"
date: 2025-12-19T20:00:00+09:00
weight: 10
bookToc: true
---
```

### 주요 Front Matter 옵션

| 옵션 | 설명 | 예시 |
|------|------|------|
| `title` | 포스트 제목 | "Hugo 시작하기" |
| `date` | 작성 날짜 | 2025-12-19T20:00:00+09:00 |
| `weight` | 메뉴 순서 (낮을수록 위) | 10 |
| `bookToc` | 목차 표시 여부 | true/false |
| `bookHidden` | 메뉴에서 숨김 | true/false |
| `bookFlatSection` | 섹션을 평평하게 표시 | true/false |
| `bookCollapseSection` | 섹션 접기 | true/false |

### 카스텀 메타데이터

검색과 SEO를 위한 추가 메타데이터:

```yaml
---
title: "포스트 제목"
description: "포스트에 대한 간단한 설명"
tags: ["hugo", "블로그", "웹개발"]
categories: ["튜토리얼"]
author: "작성자명"
---
```

## 마크다운 작성

Hugo는 표준 마크다운과 확장 기능을 지원합니다.

### 제목

```markdown
# H1 제목
## H2 제목
### H3 제목
```

### 텍스트 스타일

```markdown
**굵게**
*기울임*
~~취소선~~
`인라인 코드`
```

### 링크와 이미지

```markdown
[링크 텍스트](https://example.com)
![이미지 설명](/images/photo.jpg)
```

### 코드 블록

````markdown
```python
def hello():
    print("Hello, Hugo!")
```
````

### 리스트

```markdown
- 항목 1
- 항목 2
  - 하위 항목

1. 순서 항목 1
2. 순서 항목 2
```

### 인용

```markdown
> 인용문 내용
```

### 테이블

```markdown
| 컬럼1 | 컬럼2 |
|-------|-------|
| 내용1 | 내용2 |
```

## hugo-book Shortcodes

hugo-book 테마는 유용한 shortcode를 제공합니다.

### Hints (알림 박스)

```markdown
{{</* hint info */>}}
정보 메시지
{{</* /hint */>}}

{{</* hint warning */>}}
경고 메시지
{{</* /hint */>}}

{{</* hint danger */>}}
위험 메시지
{{</* /hint */>}}
```

### Buttons

```markdown
{{</* button relref="/" */>}}홈으로{{</* /button */>}}
{{</* button href="https://example.com" */>}}외부 링크{{</* /button */>}}
```

### Columns

```markdown
{{</* columns */>}}

## 왼쪽 컬럼
내용...

<--->

## 오른쪽 컬럼
내용...

{{</* /columns */>}}
```

### Tabs

```markdown
{{</* tabs "unique-id" */>}}
{{</* tab "탭1" */>}} 탭1 내용 {{</* /tab */>}}
{{</* tab "탭2" */>}} 탭2 내용 {{</* /tab */>}}
{{</* /tabs */>}}
```

### Details (접기/펼치기)

```markdown
{{</* details "제목" */>}}
펼쳐지는 내용
{{</* /details */>}}
```

## 이미지 관리

이미지는 `static` 디렉토리에 저장합니다:

```
static/
  images/
    photo.jpg
    logo.png
```

마크다운에서 참조:

```markdown
![설명](/images/photo.jpg)
```

## Draft 모드

작성 중인 포스트는 draft로 설정할 수 있습니다:

```yaml
---
title: "작성 중인 포스트"
draft: true
---
```

Draft 포스트를 포함하여 서버 실행:

```bash
hugo server --buildDrafts
```

## 포스트 미리보기

로컬에서 포스트를 미리 확인:

```bash
hugo server
```

브라우저에서 http://localhost:1313 접속

## 팁

1. **무게(Weight) 활용**: 포스트 순서를 weight로 조정하세요
2. **ToC 사용**: 긴 문서는 `bookToc: true`로 목차를 표시하세요
3. **Shortcode 활용**: hugo-book shortcode로 풍부한 콘텐츠 작성
4. **이미지 최적화**: 이미지는 적절한 크기로 최적화하여 사용
5. **내부 링크**: `relref` shortcode로 안전한 내부 링크 사용
