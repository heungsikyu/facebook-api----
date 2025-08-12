## 페이스북/메타 API 변경 연대표 (2015–2025)

페이스북/메타의 Graph/Marketing/Messenger/Instagram 영역별 주요 API 변경과 개발자 영향 포인트를 연도별로 간단 정리했습니다. 세부 사항은 하단의 공식 문서 링크를 참고하세요.

### 사전 배경: Open Graph 적용 시점
- 2010-04(F8): Open Graph 발표 — 웹 페이지를 소셜 그래프의 객체로 취급하는 메타태그(`og:*`)와 Like 버튼/소셜 플러그인 공개.
- 2011-09(F8): Open Graph Actions/Stories + Timeline 발표 — 앱 활동을 스토리로 퍼블리시하는 모델 도입(이후 2018 `publish_actions` 폐지로 개인 타임라인 대행 게시 불가).
- 2012~2014: 링크 미리보기/공유 품질을 위한 OG 메타태그 관행 정착(현재까지 유지).

### 2015
- 메신저 플랫폼 공개(F8) 및 기존 XMPP 기반 Chat API 종료(전환 필요)
- Graph API v2.3/2.4/2.5 등 정기 버전업 시작(이후 버전 폐기 정책의 주기 운영)

### 2016–2017
- Graph API v2.6–v2.12 릴리스(페이지, 그룹, 이벤트, 비디오 등 엔드포인트 개선)
- 앱 검수(App Review) 강화와 권한 세분화·용도 제한 고도화

### 2018
- 데이터 접근 제한 대규모 개편(Cambridge Analytica 후속)
  - 이벤트/그룹/페이지 API 접근 제약 및 대부분 엔드포인트에 앱 검수 의무화
  - Facebook Login 권한 체계 대폭 조정(민감 권한 엄격 심사)
  - `publish_actions` 권한 사용 중단(사용자 대신 게시 기능 폐지) → 공유 다이얼로그 사용 권장

### 2019
- Graph API v3.x–v5.0 릴리스, Instagram Graph/API 라인 강화
- Instagram Legacy API 단계적 종료 공지(신규/기존 개발은 Instagram Graph 또는 Basic Display로 전환)

### 2020
- Instagram Legacy API 최종 종료(6/29) → Instagram Graph API/Basic Display로 완전 전환
- iOS 14/ATT 영향 대응으로 측정/타게팅 모델 조정(마케팅 API 업데이트 동반)
- 플랫폼 약관/개발자 정책 업데이트
 - 2020-10-24: Facebook/Instagram 기존 oEmbed 임베드 중단 → Graph API `oEmbed Read`와 앱 액세스 토큰 기반 임베드로 전환 필요

### 2021
- Conversions API(서버사이드 이벤트) 적극 권장·확산: 브라우저 신호 감소 대응, 측정/최적화 보완
- Marketing API 측정/최적화 관련 업데이트 지속

### 2022–2023
- Graph API v14–v17 등 정기 버전업과 구버전 폐기 진행(버전 수명 주기 준수)
- Instagram/Messenger 엔드포인트 점진 개방(메시징, 리플라이, 미디어 인사이트 등)과 정책 정비

### 2024–2025
- Graph/Marketing API 메이저 업데이트(v18–v20대) 및 구버전 폐기 스케줄 유지
- 데이터 접근 갱신·재검수 프로세스 고도화(통합 평가/재검수 절차 개선)
- 개인 정보 보호 기조 유지, AI 관련 데이터 사용 정책 커뮤니케이션 강화

## 개발자 체크리스트(요점)
- 버전 고정 및 주기적 업그레이드: Graph/Marketing API는 일정 주기로 폐기 → 최소 연 1회 호환성 점검
- 권한 최소화·검수 대비: 2018년 이후 민감 권한은 엄격 심사 → 사용 범위/보존/고지 등 문서화 준비
- 측정 신호 이원화: 픽셀 단독 의존 지양, Conversions API와 병행 송신(중복제거 포함) 설계
- Instagram: Legacy API는 2020년 종료 → Instagram Graph API 또는 Basic Display만 사용

## 부록: `publish_actions` 권한 개요
- 정의: Facebook Login의 확장 권한으로, 앱이 사용자를 대신해 Facebook 타임라인에 게시물(텍스트/링크/사진/동영상)을 작성하도록 허용하던 권한. 주로 Graph API의 `/{user-id}/feed`, `/photos`, `/videos` 엔드포인트를 통해 사용.
- 요구사항: 사용자 주도 액션 기반 공유만 허용, 명확한 사용자 동의 및 App Review 필수, 스팸/오용 금지 정책 준수 필요.
- 폐기 일정(중요): 2018-04-24 공식 공지 이후 신규 앱은 즉시 요청 불가, 기존 승인 앱도 2018-08-01 이후 전면 중단.
- 대안:
  - 사용자 주도 공유: 플랫폼별 Facebook 공유 다이얼로그(웹/iOS/Android) 사용 권장.
  - 페이지 게시 자동화: 사용자 개인 타임라인이 아닌 Facebook 페이지에 게시가 목적이라면, Pages API와 해당 권한(예: 페이지 게시/관리 관련 권한)을 검수 후 사용.
  - 일반 웹 공유 버튼: Open Graph 메타태그를 갖춘 표준 공유 버튼 사용.
- 참고 링크: Facebook Login 변경 로그(아래 링크), 공유 다이얼로그 문서(아래 링크 참조)

> 핵심 이해
> - 사용자 타임라인 자동 게시: 불가(폐지). 사용자 권한 위임이 있어도 개인 타임라인에 대행 게시 금지.
> - 가능한 경로: 공유 다이얼로그(사용자 주도), 페이지 게시(Pages API).
> - 그룹 게시: 별도 권한/관리자 설치 등 제약이 커 정책 변동이 잦음 → 최신 문서로 요건 확인 권장.

### 대안 상세: Pages API로 페이지에 게시하기
- 핵심 개념: 개인 타임라인이 아닌 Facebook 페이지에 콘텐츠를 게시하는 용도. `/{page-id}/feed`, `/{page-id}/photos`, `/{page-id}/videos` 등을 사용하며 Page Access Token이 필요.
- 필요한 권한(권장 최소):
  - `pages_manage_posts`(필수): 페이지에 게시물/사진/동영상 게시 및 편집/삭제 권한
  - `pages_read_engagement`(조회): 게시물 읽기/인게이지먼트 조회 등
  - `pages_manage_engagement`(선택): 댓글/리액션 관리가 필요한 경우
  - `pages_manage_metadata`(선택): 구독/웹훅 설정 등 메타데이터 관리가 필요한 경우
- 접근 토큰 흐름:
  - 사용자 로그인으로 페이스북 사용자 액세스 토큰 획득 → `/me/accounts`로 사용자의 페이지 목록 및 Page Access Token 조회
  - 게시 시 Page Access Token 사용(사용자 토큰 아님)
- 앱 검수 체크리스트(요약):
  - 권한 최소 요청: 실제 필요한 권한만 요청(예: 게시만 필요하면 `pages_manage_posts` 중심)
  - 사용 사례/데모 영상: 라이브 모드 또는 테스트 사용자로 게시 흐름을 캡처한 스크린캐스트 제공
  - 정책/UX: 사용자에게 게시 주체가 "페이지"임을 명확히 고지, 연결 해제/취소 경로 제공, 스팸·강제/보상형 공유 금지
  - 기술 자료: 샘플 API 호출, 데이터 사용 목적·보존 기간 명시, 에러 처리/레이트리밋 대응 설명
  - 보안: 토큰 안전 보관, 최소 권한·최소 기간 원칙, 서버에서 민감 키 관리
- 엔드포인트 예시(개념):
  - `POST /{page-id}/feed`(링크·메시지), `POST /{page-id}/photos`, `POST /{page-id}/videos`

#### 예시 코드(간단)
주의: Page Access Token은 절대 클라이언트(브라우저)에 노출하지 마세요. 서버에서 호출하세요. 아래 `{graph-api-version}`는 현재 유효한 버전으로 고정해 사용하세요(예: `v19.0`).

```bash
# cURL: 페이지에 텍스트/링크 게시
curl -X POST \
  "https://graph.facebook.com/{graph-api-version}/{page-id}/feed" \
  -F "message=신제품이 출시되었습니다!" \
  -F "link=https://example.com/product" \
  -F "access_token={PAGE_ACCESS_TOKEN}"
```

```javascript
// Node.js (서버사이드, Node 18+ 내장 fetch): 페이지에 게시
const graphApiVersion = 'v19.0';
const pageId = process.env.FB_PAGE_ID;
const pageAccessToken = process.env.FB_PAGE_ACCESS_TOKEN; // 절대 클라이언트에 노출 금지

async function publishToPage() {
  const url = `https://graph.facebook.com/${graphApiVersion}/${pageId}/feed`;
  const params = new URLSearchParams({
    message: '신제품이 출시되었습니다!',
    link: 'https://example.com/product',
    access_token: pageAccessToken,
  });
  const res = await fetch(url, { method: 'POST', body: params });
  if (!res.ok) throw new Error(`Graph API error: ${res.status}`);
  const data = await res.json();
  return data; // { id: 'PAGE_POST_ID' }
}
```

```javascript
// 브라우저 → 백엔드 프록시(권장): 브라우저는 백엔드에 요청만 전달
// frontend
async function requestPublish() {
  const res = await fetch('/api/facebook/publish', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ message: '신제품이 출시되었습니다!', link: 'https://example.com/product' })
  });
  return res.json();
}

// backend (예: Express)
// app.post('/api/facebook/publish', async (req, res) => { ...Graph API 호출... })
```


## 공식 문서/변경 로그
- Graph API 변경 로그: [developers.facebook.com/docs/graph-api/changelog](https://developers.facebook.com/docs/graph-api/changelog/)
- Graph API 버전/폐기 정책: [developers.facebook.com/docs/graph-api/versioning](https://developers.facebook.com/docs/graph-api/versioning/)
- Facebook Login 변경 로그: [developers.facebook.com/docs/facebook-login/changelog](https://developers.facebook.com/docs/facebook-login/changelog/)
- Messenger 플랫폼 변경 로그: [developers.facebook.com/docs/messenger-platform/changelog](https://developers.facebook.com/docs/messenger-platform/changelog/)
- Instagram Basic Display API: [developers.facebook.com/docs/instagram-basic-display-api](https://developers.facebook.com/docs/instagram-basic-display-api/)
- Instagram Graph API: [developers.facebook.com/docs/instagram-api](https://developers.facebook.com/docs/instagram-api/)
- Conversions API: [developers.facebook.com/docs/marketing-api/conversions-api](https://developers.facebook.com/docs/marketing-api/conversions-api/)
- Marketing API 변경 로그: [developers.facebook.com/docs/marketing-api/changelog](https://developers.facebook.com/docs/marketing-api/changelog)
- 개발자 정책: [developers.facebook.com/devpolicy](https://developers.facebook.com/devpolicy/)
- 2018 데이터 접근 제한 공식 발표: [about.fb.com/news/2018/04/restricting-data-access](https://about.fb.com/news/2018/04/restricting-data-access/)
 - 공유 다이얼로그(웹): [developers.facebook.com/docs/sharing/reference/share-dialog](https://developers.facebook.com/docs/sharing/reference/share-dialog/)
 - Pages API 개요: [developers.facebook.com/docs/pages](https://developers.facebook.com/docs/pages)
 - 페이지 접근 토큰: [developers.facebook.com/docs/pages/access-tokens](https://developers.facebook.com/docs/pages/access-tokens/)
 - 페이지 게시 가이드: [developers.facebook.com/docs/pages/publishing](https://developers.facebook.com/docs/pages/publishing/)
 - 권한 참고: `pages_manage_posts`(필수) [docs/permissions/reference/pages_manage_posts](https://developers.facebook.com/docs/permissions/reference/pages_manage_posts), `pages_read_engagement`(조회) [docs/permissions/reference/pages_read_engagement](https://developers.facebook.com/docs/permissions/reference/pages_read_engagement), `pages_manage_engagement`(선택) [docs/permissions/reference/pages_manage_engagement](https://developers.facebook.com/docs/permissions/reference/pages_manage_engagement), `pages_manage_metadata`(선택) [docs/permissions/reference/pages_manage_metadata](https://developers.facebook.com/docs/permissions/reference/pages_manage_metadata)
 - oEmbed Read: [developers.facebook.com/docs/graph-api/reference/oembed-read](https://developers.facebook.com/docs/graph-api/reference/oembed-read/)
 - Open Graph 메타태그(ogp.me): [ogp.me](https://ogp.me/)
 - 웹 공유/OG 베스트 프랙티스: [developers.facebook.com/docs/sharing/webmasters/](https://developers.facebook.com/docs/sharing/webmasters/)

## 참고
본 문서는 핵심 변화와 영향도를 빠르게 파악하기 위한 요약입니다. 실제 적용 전에는 반드시 각 제품별 최신 공식 문서를 확인하세요.



