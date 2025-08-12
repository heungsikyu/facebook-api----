## 페이스북 내 사이트 임베드와 결제 연동(2020-10 이전) — 가능 범위와 ‘인앱결제’ 용어 구분

### 결론 요약
- 2020년 10월 이전, 페이스북 내부에 **자체 웹사이트를 임베드**(iframe)해서 **외부 PG(결제대행)**로 결제 플로우를 운영하는 것은 가능했습니다. 주로 다음 두 방식이 사용되었습니다.
  - Canvas App(캔버스 앱)
  - Page Tabs(페이지 탭, 데스크톱 중심)
- 다만 이 경우 결제는 **페이스북이 처리하는 인앱결제**가 아니라, **임베드된 웹(iframe) 안에서의 일반 웹결제**입니다.
- 페이스북에서 ‘인앱결제’라고 하면 보통 **Facebook Payments(웹 게임 결제 다이얼로그)**를 의미합니다.

---

### 임베드 방식과 결제 연동

#### 1) Canvas App(캔버스 앱)
- 의미: 페이스북 도메인 내 캔버스(전용 경로)에 앱을 **iframe**으로 로딩하는 방식(주로 웹 게임/앱).
- 결제: 앱 내부에 **외부 PG**를 붙여 일반 웹결제를 구현할 수 있었으나, **디지털 재화(게임 코인 등)** 판매에는 페이스북의 **Facebook Payments** 다이얼로그 사용이 권장/요구되었습니다.
- 근거(공식 문서):
  - Canvas Apps: https://developers.facebook.com/docs/games/canvas/
  - Facebook Payments(웹 게임 결제): https://developers.facebook.com/docs/games_payments/

#### 2) Page Tabs(페이지 탭)
- 의미: 비즈니스 페이지에 **커스텀 탭**을 추가하고 지정한 URL을 **iframe**으로 렌더링(주로 데스크톱에서 노출).
- 결제: 탭 내부에서 **일반 웹결제(외부 PG)**를 사용할 수 있었음. 다만 탭은 **데스크톱 중심**, 화면 폭/HTTPS/콘텐츠 제약 등 **정책·기술 제한**이 존재.
- 근거(공식 문서):
  - Page Tabs: https://developers.facebook.com/docs/pages/tabs
  - 제한사항(데스크톱 중심 등): https://developers.facebook.com/docs/pages/tabs#limitations

---

### ‘페이스북 인앱결제’로 볼 수 있는가?
- **아니오(대부분의 비게임/외부 PG 연동 사례)**: 임베드된 웹(iframe)에서 **외부 PG로 처리**되는 결제는 페이스북의 결제 시스템이 관여하지 않으므로, 통상 **페이스북 인앱결제**라고 부르지 않습니다.
- **예(게임 등 특정 범주)**: **Facebook Payments** 다이얼로그를 통해 결제(신용카드/페이스북 크레딧 등)한 경우는 페이스북이 제공하는 **인앱결제**에 해당합니다.

---

### 용어 정리
- 임베드 결제: 캔버스/탭 **iframe 내**에서 **외부 PG**로 처리(일반 웹결제)
- 인앱결제(IAP, Facebook Payments): **페이스북 결제 다이얼로그**로 디지털 재화/게임 재화 구매

---

### 관련 변경과 혼동 주의
- 2020-10-24의 **oEmbed 중단**은 “외부 웹사이트에서 페이스북 콘텐츠를 임베드하는 기능(무인증 oEmbed)”에 관한 변경입니다. 이는 “페이스북 내부에 내 사이트를 iframe으로 임베드(캔버스/탭)”하는 주제와 **다른 이슈**입니다.
- 근거(공식 문서):
  - Graph API oEmbed Read(토큰 필요): https://developers.facebook.com/docs/graph-api/reference/oembed-read/

---

### 체크리스트(역사적 구현 관점)
- HTTPS와 X-Frame-Options/콘텐츠 보안 정책(CSP) 설정 점검
- 탭/캔버스의 **데스크톱 중심 UX** 고려(모바일 페이스북 앱에서 탭 노출 제한 존재)
- 외부 PG의 **리다이렉트/3D Secure/팝업**이 iframe 환경에서 정상 동작하는지 사전 검증
- 페이스북 정책(스팸/오해 소지 표현/강제 공유 유도 금지) 준수

---

### 참고 링크(공식)
- Canvas Apps: https://developers.facebook.com/docs/games/canvas/
- Facebook Payments(웹 게임 결제): https://developers.facebook.com/docs/games_payments/
- Page Tabs: https://developers.facebook.com/docs/pages/tabs
- Page Tabs 제한: https://developers.facebook.com/docs/pages/tabs#limitations
- Graph API oEmbed Read: https://developers.facebook.com/docs/graph-api/reference/oembed-read/


