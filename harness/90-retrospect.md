# 90 — Retrospect (실행 로그)

> “새 모델이 오면 비계를 벗겨라.” · “하네스가 프로젝트와 싸우면 하네스를 고쳐라.”  
> 규범 템플릿: [`../HARNESS.md`](../HARNESS.md) §9. 상세 회고는 헌법 파일에도 복제·요약할 수 있다.

## 로그 형식

```
### YYYY-MM-DD · title
- **trigger**:
- **remove**:
- **add**:
- **outcome**:
```

### 2026-07-13 · Consolidate to one constitution (HARNESS v2)

- **trigger**: 주제별 분할 문서의 조회 비용 > 이득.
- **remove**: 규범 본문을 여러 파일에만 두는 방식.
- **add**: 규범은 `HARNESS.md` 단일 파일; `harness/*.md`는 **계약 인덱스·슬롯 설명**.
- **outcome**: 에이전트는 헌법 1파일 + 이 폴더의 계약 포인터.

### 2026-07-18 · Plan re-hydration (PROGRAM Harness plan)

- **trigger**: Cursor plan “개인 하네스 엔지니어링 구조” 재실행 — `harness/` 디렉터리 부재.
- **remove**: 없음 (v2 헌법 유지).
- **add**: `harness/00–90` 계약 인덱스 + `harness/templates/*` 부트스트랩 5종; 채택 근거는 아래 ADOPTION.
- **outcome**: 계획 산출물과 v2가 공존. 스택 단어는 카드에만.

---

## ADOPTION — 요소별 채택 근거 (2026-07-18)

1. **계약/카드 분리** — 하네스에 스택 단어 없음 → LMS 편향 원천 차단. 구현은 `PROJECT.md`.
2. **Evaluator 신설** — 자기평가는 관대. verify·독립 체크리스트가 벽.
3. **티어 = 실사용자·실데이터** — 스택이 아니라 위험도. Swift·단일 HTML·웹 동일 기준 (T0↔R0, T1↔R1).
4. **센서 슬롯** — 정적/동적/사람/verify는 불변, 도구는 카드가 꽂음.
5. **파일 아티팩트** — 세션 크래시·컨텍스트 리셋 생존. `@path` 핸드오프.
6. **회고 문서** — 비계 제거·하네스 결함 기록 장치.

### 범용성 스모크 (카드만으로 적합)

| 프로젝트 | 티어 | verify 슬롯 | 하네스 수정 필요? |
|---|---|---|---|
| selfLMS | T1/R1 | `npm run verify` | 없음 |
| AR app | T0/R0 | xcodebuild/수동 체크리스트 | 없음 |
| function-abstraction-simulator | T0/R0 | 브라우저 콘솔 0 | 없음 |
