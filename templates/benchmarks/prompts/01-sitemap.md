# 01. 사이트맵 작성

> **사용법**: 벤치마크의 첫 단계입니다. 아래 구분선 이후 내용을 Claude에게 지시하거나, "이 파일의 지시를 따라 진행해줘"라고 요청합니다.
> `{{변수}}`는 `benchmark.config.md` 값으로 치환합니다.

---

# 작업: {{SERVICE_NAME}} 벤치마크 1단계 — 사이트맵 작성

## 목적
{{BENCHMARK_GOAL}}을 위해 {{SERVICE_NAME}}({{SERVICE_CATEGORY}})을 벤치마크한다.
이번 단계에서는 **전체 메뉴 구조(IA)만 파악**하고, 메뉴별 상세 분석은 하지 않는다.
결과는 나중에 다른 서비스와 같은 형식으로 비교할 수 있어야 한다.

## 환경
- 크롬에 {{SERVICE_NAME}}이 로그인되어 있다. 시작 URL: {{SERVICE_URL}}
- 계정 권한: {{ACCOUNT_ROLE}} / 요금제: {{PLAN_TIER}}
- 브라우저는 Claude in Chrome으로 제어한다.
- 템플릿 위치: `{{TEMPLATE_ROOT}}`
- 결과물 위치: `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/`

## 먼저 읽을 파일
1. `{{TEMPLATE_ROOT}}/rules/safety-rules.md` — **최우선 규칙**
2. `{{TEMPLATE_ROOT}}/rules/capture-guide.md` — 파일명 규칙
3. `{{TEMPLATE_ROOT}}/taxonomy/common.csv`, `{{TEMPLATE_ROOT}}/taxonomy/{{TAXONOMY_PRESET}}` — 표준 분류
4. `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/benchmark.config.md` (있으면) — 조사 범위와 메모

## 핵심 금지사항 (규칙 파일을 못 읽어도 반드시 지킬 것)
- 발송·저장·삭제·결재·승인·초대·결제·설정 적용·출퇴근 체크·로그아웃을 하지 않는다.
- 확인 팝업은 항상 "취소"한다.
- 누르면 즉시 실행될지 애매한 버튼은 누르지 않고 나에게 묻는다.

## 할 일
1. 결과 폴더를 만들고 `{{TEMPLATE_ROOT}}/output-templates/`의 파일을 아래처럼 복사한다.
   - `sitemap.md` → `00-sitemap.md`
   - `progress.md` → `progress.md`
   - `service-README.md` → `README.md`
   - `feature-matrix.csv` → `feature-matrix.csv`
   - `insights.md` → `insights.md`
   - 복사한 파일의 `{{변수}}`를 설정값으로 치환한다.
2. GNB, LNB, 프로필 메뉴, 설정, 관리자 화면을 모두 펼쳐 **리프 메뉴(화면 단위)까지** 메뉴 트리를 만든다.
   - 접혀 있는 하위 메뉴, 탭, "더보기" 메뉴도 펼쳐서 확인한다.
   - 메뉴마다 URL 패턴(ID는 `:id`로 일반화), 필요 권한, 새 창 여부를 기록한다.
   - 메뉴마다 표준 분류(`std_category`)를 붙인다.
3. 사용자 메뉴는 `01-`부터, 관리자 메뉴는 `90-`부터 `menu_id`를 붙인다. (예: `01-mail`, `90-admin-members`)
4. 전역 구조 화면만 캡처해서 `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/00-global/screenshots/`에 저장한다.
   - 홈 화면, GNB 펼침, 프로필 메뉴, 관리자 홈, 통합 검색, 알림 센터
   - 파일명 예: `00-global_001_home.png`
   - 캡처 전 `rules/privacy-masking.md`에 따라 개인정보를 가린다.
5. `00-sitemap.md`를 채운다. 접근할 수 없는 메뉴는 이유와 함께 기록한다.
6. `progress.md`의 메뉴별 진행 표에 모든 `menu_id`를 ⬜ 상태로 등록한다.

## 보고 후 대기
작업이 끝나면 아래 내용을 보고하고 **내 승인을 기다린다.** 승인 전에는 메뉴별 상세 분석을 시작하지 않는다.
- 대메뉴 수 / 리프 메뉴 수 / 관리자 메뉴 수
- 예상 캡처 수와 권장 세션 분할안
- 접근 불가 메뉴 목록
- 판단이 필요한 사항 (범위 포함·제외, 애매한 버튼 등)

## 완료 기준
- [ ] 모든 대메뉴와 리프 메뉴가 `00-sitemap.md`에 있다
- [ ] 모든 메뉴에 `menu_id`, URL 패턴, 표준 분류가 있다
- [ ] `progress.md`에 모든 메뉴가 등록되어 있다
- [ ] 전역 구조 캡처가 저장되어 있다
