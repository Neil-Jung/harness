# Project bootstrap (새 프로젝트)

> 하네스 문서를 수정하지 않는다. **카드 1장**이 첫 산출물이다.

## 5분 (T0 / R0)

1. [`project-card.md`](project-card.md)를 프로젝트 루트 `PROJECT.md`로 복사한다.
2. §1 정체성 · §2 티어(T0) · §4.1 verify를 **체크리스트**로 채운다.
3. 끝. SPEC/SIGN-OFF는 아이디어가 커질 때.

## T1 / R1 승격 시

1. 카드 티어를 T1(R1)로 바꾸고 근거 한 문장.
2. `verify`를 **한 줄 명령**으로 만든다 (도구 자유: npm / make / xcodebuild / pytest …).
3. push 벽: pre-push(또는 CI)에서 그 명령을 실행. 우회는 명시적 env만.
4. [`../../templates/HUMAN_GATES.md`](../../templates/HUMAN_GATES.md)를 프로젝트에 두고 비우지 않는다.
5. 공개·민감이면 Evaluator 리뷰 + Security 열을 카드 §5에 켠다.

## 하네스 통제 기능 개발 시

1. [`../../templates/SPEC.md`](../../templates/SPEC.md) → 결정 포크 → 사람 `SIGN-OFF`.
2. [`sprint-contract.md`](sprint-contract.md)로 done 합의.
3. Generator 구현 → Evaluator(`evaluator-review.md` + verify).
4. 사람 게이트 → 필요 시 [`../90-retrospect.md`](../90-retrospect.md)에 마찰 기록.

## 금지

- 새 스택을 이유로 `HARNESS.md` / `harness/0x-*.md`에 도구명을 추가하기.
- 카드 없이 T1에서 “완료” 주장하기.
