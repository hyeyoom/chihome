---
title: "SEO 최적화"
weight: 4
bookToc: true
---

# SEO 최적화

검색 엔진 최적화(SEO)를 통해 블로그의 가시성을 높이는 방법을 알아봅니다.

## 기본 SEO 설정

### hugo.toml 설정

```toml
baseURL = 'https://chiho.me/'
title = 'My Blog'
languageCode = 'ko-kr'

# Google Analytics (선택사항)
googleAnalytics = 'G-XXXXXXXXXX'

# 작성자 정보
[author]
  name = '작성자명'
  email = 'email@example.com'

# 소셜 미디어
[params]
  description = '블로그 설명'
  keywords = ['키워드1', '키워드2', '키워드3']
  images = ['/images/og-image.jpg']

[params.social]
  twitter = 'username'
  github = 'username'
```

### Robots.txt

Hugo는 자동으로 robots.txt를 생성합니다. 커스터마이징하려면:

```toml
# hugo.toml
enableRobotsTXT = true
```

`layouts/robots.txt` 생성:

```
User-agent: *
Disallow: /admin/
Disallow: /private/

Sitemap: {{ .Site.BaseURL }}sitemap.xml
```

## Front Matter 최적화

각 포스트의 메타데이터를 최적화하세요:

```yaml
---
title: "명확하고 설명적인 제목 (60자 이내)"
description: "페이지 내용을 요약하는 설명 (155자 이내)"
date: 2025-12-19T20:00:00+09:00

# SEO 메타데이터
keywords: ["키워드1", "키워드2", "키워드3"]
author: "작성자명"

# Open Graph (소셜 미디어 공유)
images: ["/images/post-image.jpg"]

# 검색 엔진 크롤링 제어
robots: "index, follow"
---
```

### 제목 작성 팁

1. **길이**: 50-60자 이내
2. **키워드**: 중요한 키워드를 앞쪽에 배치
3. **고유성**: 각 페이지마다 고유한 제목
4. **의미**: 클릭을 유도하는 명확한 제목

예시:
```yaml
# 좋은 예
title: "Hugo 블로그 SEO 최적화 완벽 가이드"

# 나쁜 예
title: "블로그 포스트 1"
```

### 설명(Description) 작성 팁

1. **길이**: 120-155자
2. **요약**: 페이지 내용을 정확히 요약
3. **Call-to-Action**: 클릭을 유도하는 문구 포함

```yaml
description: "Hugo 정적 사이트에서 검색 엔진 최적화를 위한 설정 방법과 베스트 프랙티스를 상세히 설명합니다."
```

## Sitemap 설정

Hugo는 자동으로 sitemap.xml을 생성합니다.

### Sitemap 커스터마이징

```toml
# hugo.toml
[sitemap]
  changefreq = 'weekly'
  filename = 'sitemap.xml'
  priority = 0.5
```

Front Matter에서 개별 페이지 설정:

```yaml
---
title: "중요한 페이지"
sitemap:
  priority: 1.0
  changefreq: daily
---
```

## URL 구조

### Clean URLs

Hugo는 기본적으로 깔끔한 URL을 생성합니다:

```
/docs/getting-started/  (good)
/docs/getting-started.html  (not recommended)
```

### Permalinks 설정

```toml
# hugo.toml
[permalinks]
  posts = '/blog/:year/:month/:slug/'
  docs = '/docs/:slug/'
```

예시:
```
/blog/2025/12/my-post/
/docs/getting-started/
```

## 성능 최적화

### 이미지 최적화

1. **적절한 크기**: 필요한 크기로 리사이징
2. **압축**: WebP, JPEG 압축 활용
3. **Lazy Loading**: 지연 로딩 적용

```markdown
![설명](/images/photo.jpg "제목")
```

Hugo Page Resources 사용:

```
content.ko/
  docs/
    my-post/
      index.md
      featured.jpg
```

### Minification

빌드 시 자동 압축:

```toml
# hugo.toml
[minify]
  disableHTML = false
  disableCSS = false
  disableJS = false
  disableJSON = false
  disableXML = false
```

## 구조화된 데이터 (Schema.org)

### Article Schema

`layouts/_default/single.html` 또는 partial 생성:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "{{ .Title }}",
  "description": "{{ .Description }}",
  "author": {
    "@type": "Person",
    "name": "{{ .Site.Author.name }}"
  },
  "datePublished": "{{ .Date.Format "2006-01-02" }}",
  "dateModified": "{{ .Lastmod.Format "2006-01-02" }}",
  "image": "{{ .Params.images | default .Site.Params.images }}",
  "url": "{{ .Permalink }}"
}
</script>
```

## Open Graph & Twitter Cards

hugo-book 테마는 기본 Open Graph를 지원합니다. 추가 설정:

```yaml
---
title: "포스트 제목"
description: "포스트 설명"
images: ["/images/og-image.jpg"]

# Twitter Card
twitter:
  card: "summary_large_image"
  site: "@username"
---
```

## 다국어 SEO

### hreflang 태그

Hugo는 자동으로 hreflang 태그를 생성합니다:

```html
<link rel="alternate" hreflang="ko" href="https://chiho.me/ko/docs/post/" />
<link rel="alternate" hreflang="en" href="https://chiho.me/en/docs/post/" />
```

### 언어별 Sitemap

각 언어마다 별도의 sitemap이 생성됩니다:
```
/ko/sitemap.xml
/en/sitemap.xml
/sitemap.xml (통합)
```

## 콘텐츠 최적화

### 헤딩 구조

올바른 헤딩 계층 사용:

```markdown
# H1 - 페이지 제목 (하나만)

## H2 - 주요 섹션

### H3 - 하위 섹션

#### H4 - 세부 항목
```

### 내부 링크

관련 콘텐츠를 내부 링크로 연결:

```markdown
자세한 내용은 [포스트 작성하기]({{</* relref "writing-posts" */>}})를 참고하세요.
```

### 키워드 사용

- 제목과 첫 단락에 주요 키워드 포함
- 자연스럽게 본문에 키워드 분산
- 키워드 스터핑(과도한 사용) 피하기

## 분석 및 모니터링

### Google Analytics

```toml
# hugo.toml
googleAnalytics = 'G-XXXXXXXXXX'
```

### Google Search Console

1. 사이트 소유권 확인
2. Sitemap 제출: `https://chiho.me/sitemap.xml`
3. 크롤링 오류 모니터링
4. 검색 성능 분석

### 성능 측정 도구

- **Google PageSpeed Insights**: 페이지 속도 분석
- **Lighthouse**: 종합 품질 평가
- **GTmetrix**: 성능 및 최적화 제안

## 체크리스트

포스트 발행 전 확인 사항:

- [ ] 명확하고 설명적인 제목 (60자 이내)
- [ ] 적절한 description (155자 이내)
- [ ] 키워드 설정
- [ ] 이미지 alt 텍스트 추가
- [ ] 내부 링크 포함
- [ ] 올바른 헤딩 구조
- [ ] Open Graph 이미지 설정
- [ ] URL 구조 확인
- [ ] 모바일 친화성 테스트
- [ ] 페이지 로딩 속도 확인

## 추가 리소스

- [Google Search Central](https://developers.google.com/search)
- [Hugo SEO Documentation](https://gohugo.io/templates/embedded/#open-graph)
- [Schema.org](https://schema.org/)
- [Web.dev](https://web.dev/learn-core-web-vitals/)
