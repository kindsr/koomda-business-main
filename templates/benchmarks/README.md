# 웹 SaaS 벤치마크 표준 템플릿

로그인된 브라우저에서 웹 서비스(ERP, 그룹웨어, CRM, 협업툴, 쇼핑몰 관리자 등)의 화면을 모두 캡처하고, 메뉴별 기능을 분석해서 **서비스끼리 비교할 수 있는 형식**으로 정리하기 위한 프롬프트와 산출물 템플릿 모음입니다.

- 권장 설치 위치: `D:\Projects\_template\templates\benchmarks`
- 권장 실행 환경: **로컬 Claude Code + Claude in Chrome 확장** (`claude --chrome`)
  - 클라우드 세션은 사용자 PC의 크롬에 접근할 수 없으므로 반드시 로컬에서 실행합니다.

---

## 폴더 구성

| 경로 | 용도 |
|---|---|
| `benchmark.config.md` | 대상 서비스마다 채우는 변수 값 (복사해서 사용) |
| `prompts/` | Claude에게 붙여 넣을 단계별 프롬프트 |
| `rules/` | 모든 프롬프트가 공통으로 따르는 안전·개인정보·캡처 규칙 |
| `output-templates/` | 결과물 양식. 대상 서비스 폴더로 복사된 뒤 채워짐 |
| `taxonomy/` | 서비스 간 비교용 표준 기능 분류 체계 |

## 프롬프트 목록

| 파일 | 언제 쓰나 |
|---|---|
| `prompts/00-full-run.md` | 작은 서비스를 한 세션에서 끝까지 진행할 때 |
| `prompts/01-sitemap.md` | **(권장 시작점)** 전체 메뉴 구조만 먼저 파악할 때 |
| `prompts/02-menu-deep-dive.md` | 메뉴 하나씩 캡처·분석할 때 (메뉴 수만큼 반복) |
| `prompts/03-synthesis.md` | 모든 메뉴 분석이 끝난 뒤 종합 문서를 만들 때 |
| `prompts/04-cross-compare.md` | 벤치마크한 서비스 2개 이상을 비교할 때 |
| `prompts/05-resume.md` | 중간에 끊긴 작업을 이어서 할 때 |

## 권장 진행 순서

```
benchmark.config.md 작성
   │
   ▼
01-sitemap ──► 사이트맵 검토·승인
   │
   ▼
02-menu-deep-dive  ×  메뉴 수   (끊기면 05-resume)
   │
   ▼
03-synthesis
   │
   ▼
(다른 서비스도 반복)
   │
   ▼
04-cross-compare
```

큰 서비스는 `00-full-run` 하나로 끝까지 맡기기보다 **01 → 02(메뉴별) → 03**으로 나눠 실행하는 것이 좋습니다. 한 세션에 전부 맡기면 뒤쪽 메뉴일수록 분석이 얕아지는 경향이 있습니다.

---

## 변수 목록

프롬프트와 템플릿에서 `{{변수}}` 형식으로 쓰입니다. 실행 전에 `benchmark.config.md`에 값을 채우고, 프롬프트를 붙여 넣을 때 함께 첨부하거나 직접 치환합니다.

| 변수 | 설명 | 예시 |
|---|---|---|
| `{{SERVICE_NAME}}` | 서비스 표시 이름 | `Hiworks` |
| `{{SERVICE_SLUG}}` | 폴더명으로 쓰는 영문 소문자 식별자 | `hiworks` |
| `{{SERVICE_URL}}` | 시작 URL | `https://office.hiworks.com` |
| `{{SERVICE_CATEGORY}}` | 서비스 유형 | `그룹웨어/ERP` |
| `{{ACCOUNT_ROLE}}` | 로그인한 계정의 권한 | `관리자(최고 관리자)` |
| `{{PLAN_TIER}}` | 사용 중인 요금제 | `Standard` |
| `{{BENCHMARK_GOAL}}` | 이번 벤치마크의 목적 | `중소기업용 신규 그룹웨어 구상` |
| `{{BENCHMARK_DATE}}` | 조사일 (YYYY-MM-DD) | `2026-10-01` |
| `{{TEMPLATE_ROOT}}` | 이 템플릿 폴더의 경로 | `D:\Projects\_template\templates\benchmarks` |
| `{{OUTPUT_ROOT}}` | 결과물을 저장할 루트 폴더 | `D:\Projects\koomda-business-main\benchmarks` |
| `{{TAXONOMY_PRESET}}` | 추가로 쓸 분류 프리셋 파일명 (`taxonomy/` 기준) | `preset-erp-groupware.csv` |
| `{{MENU_ID}}` | `02-menu-deep-dive`에서 분석할 메뉴 ID (사이트맵 기준) | `02-approval` |
| `{{COMPARE_TARGETS}}` | `04-cross-compare`에서 비교할 서비스 slug 목록 | `hiworks, daouoffice, naverworks` |

> 산출물 템플릿에서 `<꺾쇠괄호>`로 표시된 부분은 Claude가 분석하면서 채우는 칸입니다. `{{ }}` 변수와 구분해서 사용합니다.

## 결과물 구조

```
{{OUTPUT_ROOT}}/
├── _comparisons/                      # 04-cross-compare 결과
└── {{SERVICE_SLUG}}/
    ├── README.md                      # ← output-templates/service-README.md
    ├── progress.md                    # ← output-templates/progress.md
    ├── 00-sitemap.md                  # ← output-templates/sitemap.md
    ├── feature-matrix.csv             # ← output-templates/feature-matrix.csv
    ├── insights.md                    # ← output-templates/insights.md
    ├── benchmark.config.md            # ← benchmark.config.md (값을 채운 사본)
    ├── 00-global/screenshots/         # 홈·GNB·알림 등 전역 화면 캡처
    └── {NN}-{menu-slug}/              # 예: 01-mail, 02-approval, 90-admin-members
        ├── analysis.md                # ← output-templates/menu-analysis.md
        └── screenshots/
            └── {NN}-{menu-slug}_{seq3}_{screen-desc}.png
```

---

## 빠른 시작 (Hiworks 예시)

1. `benchmark.config.md`를 결과 폴더에 복사해서 값을 채웁니다. (파일 안에 Hiworks 예시가 있습니다)
2. 크롬에서 대상 서비스에 로그인합니다.
3. 터미널에서 결과물을 저장할 프로젝트 폴더로 이동한 뒤 `claude --chrome`을 실행합니다.
4. 아래처럼 지시합니다.

```
D:\Projects\_template\templates\benchmarks\prompts\01-sitemap.md 의 지시를 따라 진행해줘.
변수 값은 D:\Projects\koomda-business-main\benchmarks\hiworks\benchmark.config.md 를 사용해.
```

5. 사이트맵을 검토하고 승인한 뒤, 메뉴마다 `02-menu-deep-dive.md`를 `{{MENU_ID}}`만 바꿔서 실행합니다.

## 실행 전 체크리스트

- [ ] 가능하면 **관리자 계정**으로 로그인했다 (관리자 설정이 기능의 상당 부분을 차지함)
- [ ] 운영 데이터가 아닌 **테스트용 회사/계정**이 있으면 그것을 사용한다
- [ ] 결과물을 커밋할 저장소가 **private**이다
- [ ] 캡처 용량이 클 경우 Git LFS 사용 여부를 정했다
- [ ] 해당 서비스 이용약관에서 화면 캡처·분석이 제한되지 않는지 확인했다
