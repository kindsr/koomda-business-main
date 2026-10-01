# 04. 서비스 간 비교

> **사용법**: 2개 이상의 서비스 벤치마크(03 단계까지)가 끝난 뒤 실행합니다. 브라우저는 쓰지 않습니다.

---

# 작업: 벤치마크 서비스 비교 분석

## 대상
- 비교 서비스: {{COMPARE_TARGETS}}
- 각 서비스 결과 위치: `{{OUTPUT_ROOT}}/<service_slug>/`
- 결과물 위치: `{{OUTPUT_ROOT}}/_comparisons/{{BENCHMARK_DATE}}/`
- 목적: {{BENCHMARK_GOAL}}

## 먼저 읽을 파일
1. 각 서비스의 `README.md`, `insights.md`, `feature-matrix.csv`, `00-sitemap.md`
2. `{{TEMPLATE_ROOT}}/taxonomy/` 아래 모든 파일

## 할 일
1. **데이터 통합**
   - 모든 서비스의 `feature-matrix.csv`를 합쳐 `merged-features.csv`를 만든다.
   - 서비스마다 조사 조건(계정 권한, 요금제, 조사일)이 다르면 README 표로 먼저 정리한다. 비교 결과를 해석할 때 이 차이를 반영한다.
2. **표준 ID 정리**
   - 서로 다른 서비스에서 같은 기능에 다른 `N` 번호가 붙었으면 하나로 합친다.
   - 2개 이상 서비스에 나온 `N` 기능은 `taxonomy-proposals.md`에 정식 표준 ID 추가 제안으로 정리한다.
3. **기능 비교표** (`feature-comparison.md`)
   - 행: `std_category` > `std_feature_id`, 열: 서비스
   - 셀: ● 있음 / ◐ 일부·제한(요금제·권한) / ○ 없음 / ? 확인 못 함
   - 분류별 기능 커버리지(%)를 요약한다.
4. **UX 비교** (`ux-comparison.md`)
   - 같은 시나리오(예: 휴가 신청, 결재 상신)의 단계 수·클릭 수를 비교한다.
   - IA 구조(메뉴 깊이, 사용자/관리자 분리 방식)를 비교한다.
   - 대표 화면 캡처를 나란히 링크한다.
5. **기회 분석** (`opportunities.md`)
   - 모든 서비스가 공통으로 가진 기능 → 기본 요건(Table stakes)
   - 일부만 가진 기능 → 차별화 요소
   - 모든 서비스가 약한 부분 → 기회 영역
   - 신규 서비스의 MVP 범위 제안 (P0/P1/P2, 근거 포함)
6. **요약** (`README.md`): 비교 조건, 핵심 결론 5개, 각 문서 링크

## 결과물
```
{{OUTPUT_ROOT}}/_comparisons/{{BENCHMARK_DATE}}/
├── README.md
├── merged-features.csv
├── feature-comparison.md
├── ux-comparison.md
├── opportunities.md
└── taxonomy-proposals.md
```

## 완료 기준
- [ ] 모든 대상 서비스의 기능이 `merged-features.csv`에 있다
- [ ] 비교표의 모든 셀이 근거 있는 값(●◐○?)으로 채워져 있다
- [ ] 결론마다 근거가 되는 서비스·메뉴·캡처가 링크되어 있다
- [ ] 조사 조건 차이가 결론에 반영되어 있다
