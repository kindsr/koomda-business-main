# 00. 전체 실행 (한 세션)

> **사용법**: 메뉴가 적은 서비스를 한 번에 진행할 때 씁니다. 메뉴가 10개를 넘는 큰 서비스는 `01 → 02(메뉴별) → 03`으로 나눠 실행하는 것을 권장합니다.
> `{{변수}}`는 `benchmark.config.md` 값으로 치환합니다.

---

# 작업: {{SERVICE_NAME}} 벤치마크 (전체)

## 목적
{{BENCHMARK_GOAL}}을 위해 {{SERVICE_NAME}}({{SERVICE_CATEGORY}})의 **모든 화면을 캡처하고 메뉴별 기능을 상세하게 분석**한다.
이후 다른 서비스도 같은 형식으로 벤치마크해서 비교할 예정이므로, 반드시 표준 템플릿과 분류 체계를 따른다.

## 환경
- 크롬에 {{SERVICE_NAME}}이 로그인되어 있다. 시작 URL: {{SERVICE_URL}}
- 계정 권한: {{ACCOUNT_ROLE}} / 요금제: {{PLAN_TIER}} / 조사일: {{BENCHMARK_DATE}}
- 브라우저는 Claude in Chrome으로 제어한다.
- 템플릿 위치: `{{TEMPLATE_ROOT}}`
- 결과물 위치: `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/`
- 분류 체계: `taxonomy/common.csv` + `taxonomy/{{TAXONOMY_PRESET}}`

## 먼저 읽을 파일
1. `{{TEMPLATE_ROOT}}/rules/safety-rules.md` — **최우선 규칙**
2. `{{TEMPLATE_ROOT}}/rules/privacy-masking.md`
3. `{{TEMPLATE_ROOT}}/rules/capture-guide.md`
4. `{{TEMPLATE_ROOT}}/output-templates/` 아래 모든 파일
5. `{{TEMPLATE_ROOT}}/taxonomy/` 아래 `README.md`, `common.csv`, `{{TAXONOMY_PRESET}}`

## 핵심 금지사항 (규칙 파일을 못 읽어도 반드시 지킬 것)
- 발송·저장·삭제·결재·승인·초대·결제·설정 적용·출퇴근 체크·로그아웃을 하지 않는다.
- 작성·설정 화면은 열어서 캡처만 하고 저장 없이 닫는다. 확인 팝업은 항상 "취소"한다.
- 누르면 즉시 실행될지 애매한 버튼은 누르지 않고 나에게 묻는다.
- 캡처 전에 개인정보를 가린다.

## 진행 단계

### 1단계: 사이트맵 → 승인 대기
`{{TEMPLATE_ROOT}}/prompts/01-sitemap.md`의 "할 일"을 수행한다.
끝나면 규모와 세션 분할안을 보고하고 **내 승인을 기다린다.**

### 2단계: 메뉴별 캡처·분석
승인 후, `progress.md`의 메뉴 순서대로 `{{TEMPLATE_ROOT}}/prompts/02-menu-deep-dive.md`의 "할 일"을 메뉴마다 반복한다.
- 메뉴 하나가 끝날 때마다 파일을 저장하고 `progress.md`를 갱신한다.
- 대메뉴 하나가 끝날 때마다 한 줄로 진행 상황을 알려준다.
- 컨텍스트가 부족해지면 현재 메뉴까지 저장하고, `05-resume.md`로 이어서 하라고 안내한 뒤 멈춘다.

### 3단계: 종합
`{{TEMPLATE_ROOT}}/prompts/03-synthesis.md`의 "할 일"을 수행한다.

## 깊이 기준
- 이 문서만 보고 **같은 화면을 다시 설계할 수 있을 정도**로 필드, 옵션값, 버튼, 상태값을 적는다.
- 모호한 표현("다양한 기능", "편리한 UI") 대신 구체적인 필드, 옵션, 클릭 수로 적는다.
- 사실과 추정을 `[확인됨]` / `[추정]` / `[실행 안 함]` / `[접근 불가]`로 구분한다.

## 완료 기준
- [ ] 사이트맵의 모든 리프 메뉴가 `progress.md`에서 ✅ 또는 ⛔다
- [ ] 모든 메뉴에 `analysis.md`가 있고 8개 항목이 채워져 있다
- [ ] 모든 기능이 표준 ID와 함께 `feature-matrix.csv`에 있다
- [ ] `insights.md`와 `README.md`가 완성되어 있다
- [ ] 캡처하지 못한 화면과 확인 필요 항목이 이유와 함께 정리되어 있다
- [ ] 끝나면 커밋할지 묻는다 (캡처 용량이 크면 Git LFS 사용 여부도 함께)
