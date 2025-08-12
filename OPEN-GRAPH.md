## Open Graph와 Facebook 공유 처리 가이드

이 문서는 Open Graph(OG)의 작동 원리와, 특정 도메인 캠페인 페이지를 페이스북 피드에 공유할 때 실제로 어떻게 처리되는지(사용자 주도 공유 플로우)를 한눈에 볼 수 있도록 정리했습니다.

### 1) Open Graph란?
- 정의: 웹페이지를 소셜 그래프의 "객체"로 설명하는 메타데이터 규격으로, 링크 공유 시 제목/설명/이미지 등 미리보기(카드)를 안정적으로 생성하기 위한 표준입니다.

### 2) 작동 원리
1. 페이지 `<head>`에 OG 메타태그 삽입
2. 사용자가 링크를 붙여넣거나 공유 다이얼로그로 공유 요청
3. 페이스북 크롤러(`facebookexternalhit/*`)가 URL을 스크랩(HTTP 요청)
4. `og:*` 태그 파싱, 이미지 등 리소스 다운받아 미리보기 카드 생성
5. 생성 결과를 페이스북 캐시에 저장(Sharing Debugger로 재스크랩 가능)

핵심 태그(최소 권장)
- `og:title`, `og:description`, `og:image`(권장 1200×630, HTTPS, 절대경로), `og:url`, `og:type`(website/article)
- 보조: `og:site_name`, `og:locale`, `og:image:width/height`, `article:*`(게시글형 메타)

예시
```html
<meta property="og:title" content="문서 제목" />
<meta property="og:description" content="요약 설명" />
<meta property="og:image" content="https://example.com/cover.jpg" />
<meta property="og:url" content="https://example.com/post" />
<meta property="og:type" content="article" />
```

폴백 규칙(플랫폼별 상이)
- OG가 없으면 `<title>`/메타 설명/본문 첫 이미지 등을 사용하는 경우가 있습니다.

주의 사항
- 크롤러 접근 차단(robots/로그인벽/지역·IP 차단) 금지, 200 응답 및 올바른 `Content-Type`
- 절대 URL/HTTPS 사용, 리다이렉트/정규화(`og:url`·canonical) 일관성 유지
- SPA는 SSR/프리렌더로 초기 HTML에 메타 포함
- 이미지 403(핫링크 차단), 과도한 용량/규격 미준수 방지

Facebook 특이점
- UA: `facebookexternalhit/*`
- 캐시 무효화: Sharing Debugger에서 “Scrape Again” 수행
- `og:image:secure_url`(HTTPS) 권장

OG vs oEmbed(개념 차이)
- OG는 페이지 메타 기반 "미리보기 카드"를 만드는 규격
- oEmbed는 콘텐츠 자체를 임베드하기 위한 API 규격(2020-10-24 이후 Graph API oEmbed Read + 앱 토큰 필요)

### 3) 특정 도메인의 캠페인 페이지를 페이스북 피드에 공유하는 흐름

준비(랜딩 URL 세팅)
- OG 메타태그 완비: `og:title/description/image/url/type` 등, HTTPS/공개 접근
- 추적 파라미터: UTM, `fbclid`(자동)로 웹 애널리틱스 집계
- 모바일 딥링크 필요 시 App Links(`al:*`) 병행 고려

공유 트리거(사용자 주도만 허용)
- 권장: Facebook Share Dialog
  - 형식: `https://www.facebook.com/dialog/share?app_id={APP_ID}&href={ENCODED_URL}&display=popup&redirect_uri={REDIRECT}`
- 대안: 사용자가 직접 링크를 붙여넣어 공유(수동)
- 자동 게시 불가: `publish_actions` 폐지(2018)로 개인 타임라인 대행 게시 금지

페이스북 측 처리
- 크롤러가 URL을 스크랩 → `og:*` 파싱 → 미리보기 생성 및 캐시
- 정책 위반(스팸/악성/저작권 등) 의심 시 도메인/URL 공유 제한·차단 가능
- 결과는 "링크 포스트" 형태로 피드에 게시되며, 도달은 알고리즘·사용자 설정에 따름(P2P 아님)

갱신/품질 관리
- 메타 변경 시 Sharing Debugger로 재스크랩(캐시 갱신)
- SSR/프리렌더 적용, 이미지 가용성(403/리디렉션 루프 방지), 응답 성능·안정성 확보
- `og:url`은 정규화된 캐논ical로 통일(UTM 허용하되 OG는 기본 URL 유지 권장)

주의 및 베스트 프랙티스
- 인센티브/강제 공유 UX, 오해 소지 메타, 저작권 위반 이미지는 정책 리스크
- 임베드(oEmbed)는 공유와 별개이며, 2020-10-24 이후 Graph API `oEmbed Read` + 앱 토큰 필요

### 4) 참고 링크
- Webmasters 공유/크롤러 가이드: `https://developers.facebook.com/docs/sharing/webmasters/`
- Facebook Crawler: `https://developers.facebook.com/docs/sharing/webmasters/crawler/`
- Sharing Debugger: `https://developers.facebook.com/tools/debug/`
- Graph API oEmbed Read: `https://developers.facebook.com/docs/graph-api/reference/oembed-read/`
- 커뮤니티 표준(스팸): `https://transparency.fb.com/policies/community-standards/spam/`
- 개발자 정책: `https://developers.facebook.com/devpolicy/`


