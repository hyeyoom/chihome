---
title: "콘텐츠 구성하기"
weight: 3
bookToc: true
---

# 콘텐츠 구성하기

블로그 콘텐츠를 효과적으로 구성하는 방법을 알아봅니다.

## 디렉토리 구조

hugo-book 테마는 계층적 디렉토리 구조를 사용합니다:

```
content.ko/
├── docs/
│   ├── _index.md          # 섹션 메인 페이지
│   ├── getting-started.md
│   ├── tutorials/          # 하위 섹션
│   │   ├── _index.md
│   │   ├── tutorial-1.md
│   │   └── tutorial-2.md
│   └── guides/
│       ├── _index.md
│       └── guide-1.md
└── posts/                  # 블로그 포스트
    ├── _index.md
    └── 2025-01-01-my-post.md
```

## 카테고리와 태그

Hugo는 Taxonomy 시스템으로 카테고리와 태그를 지원합니다.

### Front Matter에 추가

```yaml
---
title: "포스트 제목"
categories: ["튜토리얼", "개발"]
tags: ["hugo", "go", "웹개발"]
---
```

### hugo.toml 설정

카테고리와 태그를 활성화하려면:

```toml
# hugo.toml
[taxonomies]
  category = 'categories'
  tag = 'tags'
```

hugo-book 테마는 기본적으로 taxonomy를 비활성화하므로, 사용하려면 설정에서 활성화해야 합니다.

### Taxonomy 페이지

Hugo는 자동으로 다음 페이지를 생성합니다:

- `/categories/` - 모든 카테고리 목록
- `/categories/tutorial/` - "튜토리얼" 카테고리의 포스트
- `/tags/` - 모든 태그 목록
- `/tags/hugo/` - "hugo" 태그의 포스트

## 메뉴 구성

### 자동 메뉴 (File Tree)

hugo-book은 기본적으로 `content.ko/docs/` 디렉토리 구조를 기반으로 사이드바 메뉴를 자동 생성합니다.

메뉴 순서는 `weight`로 조정:

```yaml
---
title: "첫 번째 문서"
weight: 1  # 낮을수록 위에 표시
---
```

### 섹션 설정

섹션의 `_index.md`에서 섹션 동작을 제어:

```yaml
---
title: "튜토리얼"
weight: 10
bookFlatSection: false      # 하위 항목을 평평하게 표시
bookCollapseSection: true   # 기본적으로 접힌 상태
---
```

### 커스텀 메뉴

hugo.toml에서 수동으로 메뉴 정의:

```toml
[[menu.before]]
  name = "홈"
  url = "/"
  weight = 1

[[menu.after]]
  name = "GitHub"
  url = "https://github.com/yourusername"
  weight = 10
```

## 페이지 숨기기

특정 페이지를 메뉴에서 숨기기:

```yaml
---
title: "숨겨진 페이지"
bookHidden: true
---
```

## 검색에서 제외

검색 결과에서 페이지 제외:

```yaml
---
title: "검색 제외 페이지"
bookSearchExclude: true
---
```

## 다국어 콘텐츠 구성

### 디렉토리별 분리 (현재 설정)

```
content.ko/      # 한국어 콘텐츠
  docs/
    getting-started.md

content.en/      # 영어 콘텐츠
  docs/
    getting-started.md
```

### 파일명으로 분리 (대안)

```
content/
  docs/
    getting-started.ko.md
    getting-started.en.md
```

### 번역 연결

동일한 콘텐츠의 다국어 버전을 연결하려면 동일한 파일 구조를 유지하세요:

```
content.ko/docs/tutorial.md
content.en/docs/tutorial.md
```

Hugo는 자동으로 언어 전환 링크를 생성합니다.

## 정적 파일 구성

### 이미지

```
static/
  images/
    2025/
      01/
        photo.jpg
```

사용:
```markdown
![설명](/images/2025/01/photo.jpg)
```

### 다운로드 파일

```
static/
  downloads/
    document.pdf
```

링크:
```markdown
[PDF 다운로드](/downloads/document.pdf)
```

### 언어별 정적 파일

```
static/
  ko/
    images/
      banner.jpg
  en/
    images/
      banner.jpg
```

## 아카이브 구성

### 날짜별 구성

```
content.ko/
  posts/
    2025/
      01/
        post-1.md
        post-2.md
```

### 주제별 구성

```
content.ko/
  docs/
    backend/
      _index.md
      django.md
      fastapi.md
    frontend/
      _index.md
      react.md
      vue.md
```

## Front Matter 템플릿

일관된 메타데이터를 위해 `archetypes` 사용:

### archetypes/docs.md

```yaml
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
weight: 10
bookToc: true
categories: []
tags: []
---
```

새 포스트 생성:
```bash
hugo new --kind docs content.ko/docs/my-post.md
```

## 조직화 팁

1. **일관된 구조 유지**: 모든 언어에서 동일한 디렉토리 구조 사용
2. **Weight 체계**: 10, 20, 30... 처럼 간격을 두어 나중에 삽입 용이
3. **명명 규칙**: 파일명은 소문자와 하이픈 사용 (예: `my-post.md`)
4. **섹션 활용**: 관련 문서를 섹션으로 그룹화
5. **검색 최적화**: 중요한 키워드를 제목과 설명에 포함
6. **목차 활용**: 긴 문서는 `bookToc: true`로 가독성 향상
