# Evaluator review — {{CHANGE}}

> Generator와 분리된 평가. 자기 채점 금지. 도메인 열은 대상 프로젝트 `PROJECT.md` §5를 복사해 채운다.

## Meta

- **프로젝트 / 카드:**
- **범위:** (브랜치·PR·로컬 diff)
- **Risk:** R0 / R1

## A. Sensors (카드 선언분)

- [ ] `verify` 실행함 — 결과:
- [ ] static
- [ ] dynamic (해당 시)
- [ ] 사람 게이트는 **사람에게 목록으로 남김** (대신 체크 안 함)

## B. Functional

- [ ] 스프린트/스펙의 done 항목 충족
- [ ] 명시적 out-of-scope 침범 없음
- [ ] 실패·빈 상태 UX 확인 (해당 시)

## C. Regression

- [ ] 인접 플로우 스모크
- [ ] 캐시/세션/권한 경계 (해당 시)

## D. Security / domain columns

| 도메인 열 (카드에서) | 결과 pass/fail/N/A | 메모 |
|---|---|---|
| | | |

## E. UX (해당 시)

- [ ] 핵심 화면 가독·오해 소지
- [ ] AI 출력은 자동 pass 금지 — 사람 게이트로

## Verdict

- [ ] **PASS** — Generator 완료 주장 허용
- [ ] **FAIL** — 아래 피드백만으로 재작업

### Fail feedback (구체)

1.
2.
