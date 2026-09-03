# 30 — Artifacts (계약)

> 파일 통신 규약. 스택·도구 이름 금지.  
> 규범 본문: [`../HARNESS.md`](../HARNESS.md) §3.  
> 런타임 양식: [`../templates/`](../templates/) · 부트스트랩 양식: [`templates/`](templates/).

## 필수 슬롯 (하네스 통제 작업)

| 아티팩트 | 역할 |
|---|---|
| `PROJECT.md` | 티어/리스크 · verify · 사람 게이트 · 도메인 열 (카드) |
| `SPEC.md` | 매크로 계획 (SIGN-OFF 전) |
| `DECISIONS.md` | 포크마다 옵션·선택·기각 |
| `SIGN-OFF.md` | 사람 확인 + R0/R1 + Web/App/Other |
| `HUMAN_GATES.md` | R1에서 비어 있으면 안 됨 |
| `debug/DEBUG*.md` | 인간 서술 + 에이전트 재발 방지 (듀얼) |

## 프로젝트별 위치 (카드가 선언)

- 기획: 보통 `docs/plans/` 또는 루트 `SPEC.md`
- 현재 작업 메모: 프로젝트 자유 (`CURRENT_WORK.md` 등) — 카드 §6에 경로

## 핸드오프 규칙

1. 채팅만으로 상태를 넘기지 않는다 → `@상대경로`.
2. 컨텍스트 리셋 전: [`templates/handoff.md`](templates/handoff.md) 한 장.
3. 스프린트 시작 전: [`templates/sprint-contract.md`](templates/sprint-contract.md)로 done 정의.

## Micro 예외

Activation gate에 해당하는 미세 수정은 SPEC/SIGN-OFF 전체 루프를 강제하지 않는다.  
그래도 **완료 주장**은 카드의 verify(또는 T0 체크리스트)를 거친다.
