# 03. 종합 분석

> **사용법**: 모든 메뉴가 ✅(또는 ⛔)가 된 뒤 실행합니다. 브라우저는 필요할 때만 확인용으로 씁니다.

---

# 작업: {{SERVICE_NAME}} 벤치마크 3단계 — 종합 분석

## 목적
메뉴별 분석 결과를 종합해서 {{BENCHMARK_GOAL}}에 바로 쓸 수 있는 결론을 만든다.

## 먼저 읽을 파일
1. `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/progress.md` — 미완료 메뉴가 있는지 확인
2. `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/00-sitemap.md`
3. `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/*/analysis.md` — 모든 메뉴 분석
4. `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/feature-matrix.csv`
5. `{{TEMPLATE_ROOT}}/output-templates/insights.md`, `{{TEMPLATE_ROOT}}/output-templates/service-README.md`

## 할 일
1. **누락 확인**: `progress.md`에 ⬜·🔄 메뉴가 있으면 목록을 보고하고 계속할지 묻는다.
2. **기능 매트릭스 정리**
   - 중복 행을 합치고, 표준 ID 매핑이 일관적인지 확인한다.
   - `N` 번호 기능을 모아 "신규 후보 기능" 목록을 만든다.
   - CSV가 올바르게 파싱되는지 확인한다. (컬럼 수 일치, 쉼표 값 따옴표 처리)
3. **insights.md 작성**: 10개 항목을 모두 채운다.
   - 강점·약점은 각각 최대 10개, 모두 근거 문서·캡처를 링크한다.
   - 공통 UI 컴포넌트 패턴은 여러 메뉴에 반복해서 나오는 것만 적는다.
   - 메뉴 간 연동은 각 `analysis.md`의 6번 항목을 모아 Mermaid 다이어그램 하나로 그린다.
   - 기회 요소와 MVP 후보는 {{BENCHMARK_GOAL}} 관점에서 우선순위를 매긴다.
4. **README.md 완성**: 규모 수치, 핵심 발견 Top 5, 메뉴별 문서 표, 조사 한계를 채운다.
5. **품질 점검**
   - 모든 `analysis.md`의 캡처 링크가 실제 파일을 가리키는지 확인한다.
   - 파일명에 `_UNMASKED`가 붙은 캡처 목록을 보고한다.
   - "다양한", "편리한" 같은 모호한 표현이 남아 있으면 구체적으로 고친다.
6. `progress.md`에서 "3. 종합"을 ✅로 바꾼다.

## 보고
- 전체 규모 요약 (메뉴·캡처·기능 수)
- 핵심 발견 Top 5
- MVP 후보 P0 목록
- 확인 필요 항목과 `_UNMASKED` 캡처 목록
- 커밋 여부 질문 (캡처 용량이 크면 Git LFS 사용 여부도 함께 묻는다)

## 완료 기준
- [ ] `insights.md` 10개 항목이 근거와 함께 채워져 있다
- [ ] `README.md`의 수치가 실제 파일 수와 일치한다
- [ ] `feature-matrix.csv`가 오류 없이 파싱된다
- [ ] 깨진 캡처 링크가 없다
