# 벤치마크 설정

> 이 파일을 `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/benchmark.config.md`로 복사해서 값을 채운 뒤 사용합니다.
> 각 프롬프트는 이 파일의 값으로 `{{변수}}`를 치환해서 실행합니다.

## 설정값

| 변수 | 값 |
|---|---|
| `SERVICE_NAME` | |
| `SERVICE_SLUG` | |
| `SERVICE_URL` | |
| `SERVICE_CATEGORY` | |
| `ACCOUNT_ROLE` | |
| `PLAN_TIER` | |
| `BENCHMARK_GOAL` | |
| `BENCHMARK_DATE` | |
| `TEMPLATE_ROOT` | `D:\Projects\_template\templates\benchmarks` |
| `OUTPUT_ROOT` | |
| `TAXONOMY_PRESET` | |

## 조사 범위

- 포함: <예: 사용자 메뉴 전체, 관리자 메뉴 전체, 개인 설정>
- 제외: <예: 모바일 앱, 외부 연동 마켓플레이스, 결제 화면>
- 특히 깊게 볼 메뉴: <예: 전자결재, 근태>

## 메모

- <계정·데이터 상태 등 Claude가 알아야 할 사항. 예: 테스트 회사라 결재 문서가 거의 없음>

---

## 예시: Hiworks

| 변수 | 값 |
|---|---|
| `SERVICE_NAME` | `Hiworks` |
| `SERVICE_SLUG` | `hiworks` |
| `SERVICE_URL` | `https://office.hiworks.com` |
| `SERVICE_CATEGORY` | `그룹웨어/ERP` |
| `ACCOUNT_ROLE` | `관리자(최고 관리자)` |
| `PLAN_TIER` | `<사용 중인 요금제>` |
| `BENCHMARK_GOAL` | `중소기업용 신규 그룹웨어/ERP 서비스 구상을 위한 기능·UX 벤치마크` |
| `BENCHMARK_DATE` | `2026-10-01` |
| `TEMPLATE_ROOT` | `D:\Projects\_template\templates\benchmarks` |
| `OUTPUT_ROOT` | `D:\Projects\koomda-business-main\benchmarks` |
| `TAXONOMY_PRESET` | `preset-erp-groupware.csv` |

- 포함: 사용자 메뉴 전체, 관리자 메뉴 전체, 개인 설정
- 제외: 모바일 앱, 결제·요금제 변경 화면(열람만)
- 특히 깊게 볼 메뉴: 전자결재, 근태·휴가, 경비
