# 02. 메뉴별 캡처·분석

> **사용법**: 사이트맵 승인 후, 메뉴 하나마다 실행합니다. `{{MENU_ID}}`만 바꿔서 반복합니다.
> 한 세션에 대메뉴 2~3개 정도가 적당합니다. 여러 메뉴를 이어서 할 때는 "`progress.md`의 다음 ⬜ 메뉴를 진행해줘"라고 요청해도 됩니다.

---

# 작업: {{SERVICE_NAME}} 벤치마크 2단계 — `{{MENU_ID}}` 메뉴 분석

## 목적
{{BENCHMARK_GOAL}}을 위해 {{SERVICE_NAME}}의 `{{MENU_ID}}` 메뉴와 그 하위 메뉴를 **빠짐없이 캡처하고 기능을 상세하게 분석**한다.
분석 결과는 다른 서비스와 같은 형식으로 비교할 수 있어야 한다.

## 환경
- 크롬에 {{SERVICE_NAME}}이 로그인되어 있다. 계정 권한: {{ACCOUNT_ROLE}} / 요금제: {{PLAN_TIER}}
- 템플릿 위치: `{{TEMPLATE_ROOT}}`
- 결과물 위치: `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/{{MENU_ID}}/`

## 먼저 읽을 파일
1. `{{TEMPLATE_ROOT}}/rules/safety-rules.md` — **최우선 규칙**
2. `{{TEMPLATE_ROOT}}/rules/privacy-masking.md`
3. `{{TEMPLATE_ROOT}}/rules/capture-guide.md`
4. `{{TEMPLATE_ROOT}}/output-templates/menu-analysis.md`
5. `{{TEMPLATE_ROOT}}/taxonomy/common.csv`, `{{TEMPLATE_ROOT}}/taxonomy/{{TAXONOMY_PRESET}}`, `{{TEMPLATE_ROOT}}/taxonomy/README.md`
6. `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/00-sitemap.md` — 이 메뉴의 하위 구조
7. `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/progress.md` — 이미 진행된 부분이 있는지 확인

## 핵심 금지사항 (규칙 파일을 못 읽어도 반드시 지킬 것)
- 발송·저장·삭제·결재·승인·초대·결제·설정 적용·출퇴근 체크·로그아웃을 하지 않는다.
- 작성·설정 화면은 열어서 캡처만 하고 저장 없이 닫는다. 확인 팝업은 항상 "취소"한다.
- 누르면 즉시 실행될지 애매한 버튼은 누르지 않고 `progress.md`의 "확인 필요"에 적는다.
- 캡처 전에 개인정보를 가린다.

## 할 일
1. `progress.md`에서 이 메뉴를 🔄로 바꾼다.
2. `menu-analysis.md` 템플릿을 `{{MENU_ID}}/analysis.md`로 복사하고 `{{변수}}`를 치환한다.
3. 사이트맵의 하위 메뉴를 순서대로 돌면서, `capture-guide.md`의 **화면 상태 15가지** 중 해당되는 것을 모두 캡처한다.
   - 저장 위치: `{{MENU_ID}}/screenshots/`
   - 파일명: `{{MENU_ID}}_{seq3}_{screen-desc}.png`
   - 캡처할 때마다 `analysis.md`의 화면 목록에 한 줄 추가한다.
4. 화면을 보면서 `analysis.md`의 8개 항목을 채운다.
   - **기능 상세**: 입력 필드는 필드명·타입·필수 여부·기본값·**옵션값 전체**를 적는다. 드롭다운은 펼쳐서 모든 옵션을 기록한다.
   - **버튼·액션**: 화면의 모든 버튼을 적는다. 실행하지 않은 버튼은 `[실행 안 함]`으로 표시하고 결과를 추정해 적는다.
   - **업무 흐름**: 이 메뉴의 대표 시나리오 1~3개를 Mermaid flowchart와 단계 목록으로 적고, 클릭 수를 센다.
   - **데이터 모델**: 필드와 관계를 근거로 Mermaid ER 다이어그램을 그린다.
   - **연동**: 다른 메뉴로 데이터가 넘어가는 지점을 찾는다.
   - **UX 관찰**과 **신규 서비스 관점 메모**는 근거 화면을 반드시 적는다.
5. 기능마다 표준 기능 ID(`std_feature_id`)를 붙이고, `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/feature-matrix.csv`에 행을 추가한다.
   - `service` 컬럼에는 `{{SERVICE_SLUG}}`, `menu_id` 컬럼에는 `{{MENU_ID}}`를 넣는다.
   - 표준 목록에 없는 기능은 `taxonomy/README.md`의 규칙대로 `N` 번호를 붙인다.
   - `evidence`에는 `확인됨` / `추정` / `실행 안 함` / `접근 불가` 중 하나를 넣는다.
   - 쉼표가 들어간 값은 큰따옴표로 감싼다.
6. **하위 메뉴 하나를 끝낼 때마다** 파일을 저장하고 `progress.md`의 "마지막 작업 화면"을 갱신한다. (작업이 끊겨도 이어서 할 수 있게)
7. 메뉴가 끝나면 `progress.md`에서 ✅로 바꾸고 캡처 수·기능 수를 적는다.

## 깊이 기준
"최대한 디테일하게"의 기준은 다음과 같다.
- 이 문서만 보고 **같은 화면을 다시 설계할 수 있을 정도**로 필드와 동작을 적는다.
- "다양한 기능 제공", "편리한 UI" 같은 모호한 표현은 쓰지 않는다. 구체적인 필드, 옵션, 버튼, 클릭 수로 적는다.
- 추정한 내용은 반드시 `[추정]`으로 표시하고 근거를 적는다.

## 보고
메뉴가 끝나면 짧게 보고한다.
- 캡처 수 / 기능 수 / `[확인됨]`·`[추정]`·`[실행 안 함]`·`[접근 불가]` 개수
- 눈에 띄는 발견 3가지
- "확인 필요"에 추가한 항목

## 완료 기준
- [ ] 사이트맵상 이 메뉴의 모든 하위 메뉴를 다뤘다
- [ ] 해당되는 화면 상태를 모두 캡처했고, 개인정보가 가려져 있다
- [ ] `analysis.md`의 8개 항목이 모두 채워져 있다 (해당 없으면 "해당 없음"과 이유)
- [ ] 모든 기능이 `feature-matrix.csv`에 표준 ID와 함께 들어가 있다
- [ ] `progress.md`가 ✅로 갱신되어 있다
