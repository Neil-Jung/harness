# 20 — Roles (계약)

> 스택 중립. Planner / Generator / Evaluator 책임만 정의한다.  
> 규범 본문: [`../HARNESS.md`](../HARNESS.md) §4.

## Planner

- **보장:** 구현 전 스펙·결정·위험/플랫폼 선택이 파일로 존재한다.
- **산출:** `SPEC.md` · `DECISIONS.md` · (사람) `SIGN-OFF.md` · 필요 시 `docs/plans/*-architecture.md`
- **등급:** strongest reasoning (제품명 고정 금지).
- **깊이 (MUST):** SPEC은 작업 순서 나열이 아니다. mid-tier Implementer가 스스로 추론하기 어려운 **코딩 스킬·불변조건·안티패턴**과 **엣지케이스 + 수용 확인 방법**을 파일에 명시한다. 프로세스만 있으면 계획 실패로 보고 다시 쓴다.

## Generator

- **보장:** SIGN-OFF(또는 micro 예외) 이후, 카드/스펙에 맞게 구현한다.
- **금지:** 자기 구현을 최종 “완료·안전”으로 승인하는 것.
- **핸드오프:** `@architecture.md` / `@SPEC.md` 등 파일 경로.
- **등급:** mid-tier OK.

## Evaluator

- **보장:** Generator와 **분리된** 검증. 카드에 선언된 센서(`verify`, 정적/동적)를 실행한다.
- **산출:** 통과 증거(명령 출력) 또는 `templates/evaluator-review.md` 체크리스트.
- **실패 시:** 구체 피드백 → Generator로 되돌림. “로컬에선 됐다”로 스킵 금지.
- **등급:** strongest reasoning (제품명 고정 금지).

## 사람

- R1/T1: `HUMAN_GATES.md` / 카드 §사람 게이트. 에이전트가 대신 체크하지 않는다.
