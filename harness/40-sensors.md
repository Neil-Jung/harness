# 40 — Sensors (계약)

> **슬롯은 불변, 도구는 가변.** 하네스는 “무엇을 보장할지”만 정하고, 명령은 `PROJECT.md`가 꽂는다.  
> 규범: [`../HARNESS.md`](../HARNESS.md) §4 Review · Stage 5.

## 슬롯

| 슬롯 | 보장 | 구현 예 (카드가 채움 — 여기 적지 않음) |
|---|---|---|
| **verify** | “완료/ push” 전 한 번에 돌리는 벽 | 프로젝트마다 1개 명령 또는 T0 체크리스트 |
| **static** | 머지 전 자동·빠른 결함 | 린트·타입·정적 보안 규칙… |
| **dynamic** | 동작·회귀 | 단위/통합/E2E·빌드 실행… |
| **human** | 자동 불가·비가역 | prod 스키마, 실계정 smoke, UX/AI 품질… |

## 규칙

1. R1/T1: `verify`는 push 전 실행되어야 한다 (git hook 권장, 우회는 명시적 env).
2. 센서 실패 = 벽. Generator가 “나중에”로 닫지 않는다.
3. 사람 게이트는 에이전트 혼자 `done` 처리 금지.
4. 새 스택 추가 시 **이 파일을 고치지 않는다** — 카드만 작성. 안 맞으면 하네스 결함 → [`90-retrospect.md`](90-retrospect.md).

## Evaluator 연결

독립 평가 시 [`templates/evaluator-review.md`](templates/evaluator-review.md) + 카드 §도메인 열을 사용한다.
