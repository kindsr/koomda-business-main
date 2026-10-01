# 05. 중단된 작업 이어서 하기

> **사용법**: 세션이 끊기거나 컨텍스트가 넘쳐서 새 세션을 열었을 때 실행합니다.

---

# 작업: {{SERVICE_NAME}} 벤치마크 이어서 진행

## 할 일
1. 아래 파일을 읽고 현재 상태를 파악한다.
   - `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/progress.md`
   - `{{OUTPUT_ROOT}}/{{SERVICE_SLUG}}/benchmark.config.md`
   - `{{TEMPLATE_ROOT}}/rules/safety-rules.md` — **최우선 규칙**
2. 🔄 상태인 메뉴가 있으면
   - 해당 메뉴의 `analysis.md`와 `screenshots/` 폴더를 확인해서 어디까지 진행됐는지 파악한다.
   - "마지막 작업 화면" 다음부터 이어서 진행한다. 이미 캡처한 화면은 다시 캡처하지 않는다.
   - 캡처 순번(`seq3`)은 기존 마지막 번호 다음부터 이어서 붙인다.
3. 🔄 메뉴가 없으면 다음 ⬜ 메뉴부터 진행한다.
4. 진행 방법은 단계에 맞는 프롬프트를 따른다.
   - 사이트맵 미완료 → `{{TEMPLATE_ROOT}}/prompts/01-sitemap.md`
   - 메뉴 분석 중 → `{{TEMPLATE_ROOT}}/prompts/02-menu-deep-dive.md`
   - 모든 메뉴 완료 → `{{TEMPLATE_ROOT}}/prompts/03-synthesis.md`
5. 브라우저 로그인이 풀려 있으면 작업을 멈추고 다시 로그인해 달라고 요청한다.

## 시작 전 보고
진행하기 전에 아래 내용을 짧게 보고한다. 별도 지시가 없으면 보고 후 바로 이어서 진행한다.
- 완료 / 진행 중 / 남은 메뉴 수
- 이어서 시작할 메뉴와 화면
- "확인 필요" 목록에 내가 답해야 할 항목이 있는지
