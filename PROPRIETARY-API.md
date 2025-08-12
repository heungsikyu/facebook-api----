## 페이스북(메타) 독점적 API의 의미와 근거 정리

페이스북/메타의 "독점적(프로프라이어터리) API"가 의미하는 바를 정의하고, 이를 뒷받침하는 공식 문서 근거를 정리합니다.

### 1) 정의
- 독점적 API: 메타가 소유·관리하며 접근 조건, 사용 범위, 데이터 처리 규칙을 메타의 정책·심사(App Review)·권한 체계로 통제하는 인터페이스. 공개 표준이 아닌 메타 고유 규칙과 버전 정책을 따릅니다.

### 2) 통제 메커니즘(근거)
- 권한·기능 검수(App Review)
  - 권한/기능은 App Review로 승인 받아야 사용 가능: [App Review 안내](https://developers.facebook.com/docs/apps/review/)
  - 권한 레퍼런스(세분화된 권한 목록과 요구사항): [Permissions Reference](https://developers.facebook.com/docs/permissions/reference)
- 비즈니스 인증·데이터 사용 점검
  - 일부 권한은 비즈니스 인증·기업 확인 필요: [Business Verification](https://www.facebook.com/business/help/2058515294227817)
  - 주기적 데이터 사용 점검 프로그램: [Data Use Checkup](https://developers.facebook.com/docs/privacy-and-data-policies/data-use-checkup/)
- 정책 준수 의무와 집행
  - 플랫폼 정책(데이터 보존·재사용 제한 등): [Developer Policies](https://developers.facebook.com/devpolicy/)
  - 커뮤니티 표준(스팸/오용 차단): [Community Standards – Spam](https://transparency.fb.com/policies/community-standards/spam/)
- 레이트 리밋·감사
  - 호출 제한 및 제재 가능: [Graph API Rate Limiting](https://developers.facebook.com/docs/graph-api/overview/rate-limiting/)
- 버전 관리·폐기 정책
  - 버전 주기, 지원 종료·브레이킹 변경 관리: [Graph API Versioning](https://developers.facebook.com/docs/graph-api/versioning/), [Changelog](https://developers.facebook.com/docs/graph-api/changelog/)
- 제한 제공(Limited Availability) 사례
  - 민감 데이터 권한은 심사·특별 요건: 예) Page Public Content Access: [page_public_metadata_access / page_public_content_access](https://developers.facebook.com/docs/graph-api/reference/page)
  - oEmbed 임베드도 앱 토큰·API 전환(접근 통제 강화): [oEmbed Read](https://developers.facebook.com/docs/graph-api/reference/oembed-read/)

### 3) 변경·폐기 사례(근거)
- `publish_actions` 권한 폐지(2018-04-24 공지, 2018-08-01 중단): [Facebook Login 변경 로그](https://developers.facebook.com/docs/facebook-login/changelog/)
- 2020-10-24 기존 oEmbed 중단 → Graph API `oEmbed Read` 필요: [oEmbed Read 문서](https://developers.facebook.com/docs/graph-api/reference/oembed-read/)

### 4) 오픈 표준과의 대비(근거)
- Open Graph 메타태그는 페이지가 자가 선언하는 메타데이터(상대적으로 개방): [OGP 공식 사이트](https://ogp.me/), [Facebook Webmasters 가이드](https://developers.facebook.com/docs/sharing/webmasters/)
- 반면 Graph/Marketing/Instagram/Messenger API는 메타의 권한·검수·정책에 의해 통제되는 독점적 인터페이스(위 문서들 참조).

### 5) 개발 시 유의점(체크리스트)
- 필요한 권한만 최소 요청(App Review 준비: 사용 사례, 동의 화면, 데모 영상, 보안 설계)
- 데이터 보존·2차 활용 제한, 사용자 고지·동의, 삭제 요청 처리(정책 준수)
- 버전 고정 및 지원 종료 모니터링(Changelog/Versioning 구독)
- 레이트 리밋 대응(백오프/큐잉), 에러 코드별 재시도 정책
- 주기적 Data Use Checkup, 비즈니스 인증 상태 유지

### 6) 참고 링크(공식)
- App Review: [developers.facebook.com/docs/apps/review](https://developers.facebook.com/docs/apps/review/)
- Permissions Reference: [developers.facebook.com/docs/permissions/reference](https://developers.facebook.com/docs/permissions/reference)
- Developer Policies: [developers.facebook.com/devpolicy](https://developers.facebook.com/devpolicy/)
- Graph API Versioning: [developers.facebook.com/docs/graph-api/versioning](https://developers.facebook.com/docs/graph-api/versioning/)
- Graph API Changelog: [developers.facebook.com/docs/graph-api/changelog](https://developers.facebook.com/docs/graph-api/changelog/)
- Rate Limiting: [developers.facebook.com/docs/graph-api/overview/rate-limiting](https://developers.facebook.com/docs/graph-api/overview/rate-limiting/)
- Data Use Checkup: [developers.facebook.com/docs/privacy-and-data-policies/data-use-checkup](https://developers.facebook.com/docs/privacy-and-data-policies/data-use-checkup/)
- oEmbed Read: [developers.facebook.com/docs/graph-api/reference/oembed-read](https://developers.facebook.com/docs/graph-api/reference/oembed-read/)
- Webmasters(OG/스크랩): [developers.facebook.com/docs/sharing/webmasters](https://developers.facebook.com/docs/sharing/webmasters/)


