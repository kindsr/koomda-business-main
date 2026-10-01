# 개인정보 마스킹 규칙

벤치마크 결과물(캡처·문서)은 저장소에 커밋되고 다른 사람과 공유될 수 있습니다. **UI 구조와 레이블은 보이게, 실제 사람과 회사의 정보는 가리는 것**이 원칙입니다.

## 1. 가려야 하는 정보

- 사람: 실명, 프로필 사진, 이메일 주소, 전화번호, 사번, 생년월일, 주소
- 내용: 메일 본문·제목, 메시지, 결재 문서 본문, 게시글 본문, 첨부파일명, 댓글
- 회사: 회사명, 사업자번호, 계좌번호, 금액이 들어간 실제 거래 내역
- 보안: API 키, 토큰, 초대 링크, QR 코드, IP 주소

## 2. 가리지 않는 정보

- 메뉴명, 버튼명, 컬럼 헤더, 필드 레이블, 안내 문구, 플레이스홀더
- 상태값(예: "결재 대기"), 아이콘, 배지, 레이아웃
- 서비스 자체의 브랜드·로고 (벤치마크 대상 식별에 필요)

## 3. 캡처 전 마스킹 방법

캡처하기 직전에 브라우저 콘솔(또는 Claude in Chrome의 JS 실행)로 아래 스니펫을 실행합니다. 화면에서만 적용되고 서버 데이터는 바뀌지 않습니다.

```js
// 1) 화면별로 개인정보가 들어간 요소의 셀렉터를 지정한다.
//    (개발자 도구로 구조를 보고 테이블 셀, 이름 영역, 본문 영역 등을 골라 넣는다)
const SELECTORS = [
  // 예시: 'td.name', '.mail-subject', '.profile-img', '.content-body'
];

// 2) 셀렉터에 해당하는 요소를 흐리게 처리한다.
SELECTORS.forEach(sel =>
  document.querySelectorAll(sel).forEach(el => {
    el.style.filter = 'blur(6px)';
    el.dataset.benchmarkMasked = '1';
  })
);

// 3) 이메일·전화번호 패턴이 들어간 텍스트 노드를 추가로 찾아 흐리게 처리한다.
const PATTERNS = [
  /[\w.+-]+@[\w-]+\.[\w.-]+/,            // 이메일
  /01[016789][-\s]?\d{3,4}[-\s]?\d{4}/,  // 휴대폰
  /\d{2,3}[-\s]\d{3,4}[-\s]\d{4}/,       // 일반 전화
];
const walker = document.createTreeWalker(document.body, NodeFilter.SHOW_TEXT);
while (walker.nextNode()) {
  const node = walker.currentNode;
  if (PATTERNS.some(p => p.test(node.textContent)) && node.parentElement) {
    node.parentElement.style.filter = 'blur(6px)';
    node.parentElement.dataset.benchmarkMasked = '1';
  }
}
```

마스킹을 되돌릴 때:

```js
document.querySelectorAll('[data-benchmark-masked]').forEach(el => {
  el.style.filter = '';
  delete el.dataset.benchmarkMasked;
});
```

## 4. 확인 절차

1. 마스킹을 적용한 뒤 캡처한다.
2. 캡처 이미지를 다시 열어 가려지지 않은 개인정보가 없는지 확인한다.
3. 가려지지 않은 정보가 있으면 셀렉터를 추가해서 다시 캡처한다.
4. iframe 안의 내용(메일 본문 등)은 iframe 문서에도 같은 스니펫을 실행해야 한다.
5. 마스킹이 어려운 화면은 캡처 파일명 끝에 `_UNMASKED`를 붙이고 `progress.md`의 "확인 필요" 목록에 남긴다. 사용자가 확인하기 전까지 커밋하지 않는다.

## 5. 문서 작성 시

- 분석 문서에는 실제 이름·내용 대신 `홍길동`, `(주)예시회사`, `user@example.com` 같은 더미 값을 쓴다.
- 입력 필드의 옵션값(예: 결재 양식 이름, 부서 목록)이 회사 고유 정보라면 `<회사 정의 양식 1>`처럼 일반화한다.
