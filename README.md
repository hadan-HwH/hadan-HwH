### Hadan

**문서 뒤의 구조를 직접 만드는 PM**

기획이 문서 더미 속에서 낡아가지 않도록 스키마·그래프·검증 게이트 같은 구조로 만들고, 필요한 도구는 직접 만듭니다.
코드보다 문서를 먼저 씁니다. 수식, 엣지 케이스, 화면 명세까지 확정한 다음에 구현합니다.

---

#### Projects

| | |
|---|---|
| **[product-planning-ir](https://github.com/hadan-HwH/product-planning-ir)**<br/>`Python` `YAML Schema` `Claude Skills` | 기획 지식을 문서가 아니라 **타입 있는 atom 그래프(SSOT)**로 관리하고, 사람이 읽는 문서는 거기서 컴파일합니다. 모든 변경은 Proposal → 검증 → merge 경로로만 들어가고, 모르는 건 지어내지 않고 `OpenQuestion`으로 남깁니다. 결정을 이벤트 스트림으로 기록하고 "지금 유효한 결정"을 reducer로 계산합니다. 덕분에 이미 뒤집힌 결정이 현재 결정처럼 섞이는 RAG의 문제를 막습니다(합성 픽스처에서 오염률 0.80 → 0.00). |
| **[polly-bot](https://github.com/hadan-HwH/polly-bot)**<br/>`Python` `FastAPI` `React` `TypeScript` | Polymarket 다중 선택 이벤트에서 **N개 아웃컴을 한 세트로 묶어** 차익을 계산하는 탐지 엔진과 실시간 대시보드입니다. 기존 오픈소스는 YES/NO 2개짜리 마켓만 봤는데, 이 엔진은 k개 아웃컴 전체와 NegRisk 변환(NO 1개 = 나머지 k−1개의 YES)까지 계산합니다. |

#### How I work

- **문서가 먼저, 코드는 그다음.** 전략 문서에서 수식과 엣지 케이스를 닫은 다음 Phase로 나눠 구현합니다.
- **AI와 일할 때는 규칙을 시스템에 박습니다.** 근거 없는 내용은 생성하지 않고 미결로 남기며, 그 규칙을 검증기로 강제합니다.
- **확인된 것만 믿습니다.** 스키마·참조 감사(audit), 회귀·뮤테이션 테스트를 merge 게이트로 둡니다.
