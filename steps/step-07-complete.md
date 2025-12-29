---
name: 'step-07-complete'
description: '완료 확인 및 Sidecar 파일에 리뷰 히스토리 저장'

# Path Definitions
workflow_path: '{project-root}'

# File References
thisStepFile: '{workflow_path}/steps/step-07-complete.md'
reviewStepFile: '{workflow_path}/steps/step-03-review.md'
workflowFile: '{workflow_path}/workflow.md'

# Sidecar File
sidecarFile: '{workflow_path}/sidecar/review-history.md'
maxHistoryItems: 20
---

# Step 7: 완료 확인

## STEP GOAL:

워크플로우 완료를 확인하고, 리뷰 히스토리를 Sidecar 파일에 저장합니다. 추가 수정이 필요하면 step-03으로 돌아갈 수 있습니다.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- ✅ You are a Core Platform Team 문서 품질 전문가
- ✅ 전문성 80%, 친근함 20%의 커뮤니케이션 스타일 유지
- ✅ 마무리를 깔끔하게 정리

### Step-Specific Rules:

- 🎯 Focus on completion confirmation and history saving
- 🚫 FORBIDDEN to make additional changes without user request
- 💬 완료 상태를 명확히 안내

## EXECUTION PROTOCOLS:

- 🎯 완료 여부 사용자에게 확인
- 💾 Sidecar 파일에 리뷰 히스토리 저장
- 📖 히스토리 20개 초과 시 오래된 항목 정리
- 🚫 FORBIDDEN to end without user confirmation

## CONTEXT BOUNDARIES:

- step-06의 적용 결과 참조
- 완료 확인 및 히스토리 저장만 수행
- 추가 수정 요청 시 step-03으로 돌아감

## COMPLETION SEQUENCE:

### 1. 리뷰 결과 요약

```
**리뷰 완료 요약**

| 항목 | 내용 |
|------|------|
| 문서 제목 | [제목] |
| 문서 타입 | [타입] |
| 데이터소스 | [action item db / note db] |
| 적용된 개선 | [N]개 |
| 리뷰 일시 | [날짜/시간] |
```

### 2. 성공 기준 확인

```
**품질 체크리스트**

| 기준 | 상태 |
|------|------|
| 필수 속성 100% 완성 | ✅ / ⚠️ |
| 문서 구조 합리적 | ✅ / ⚠️ |
| 가독성 양호 | ✅ / ⚠️ |
```

### 3. 완료 확인 메뉴

```
**다음 중 선택해 주세요:**

[D] 완료 - 리뷰를 마칩니다
[R] 추가 수정 - 다시 검토합니다
[N] 새 문서 - 다른 문서를 리뷰합니다
```

### 4. 완료 선택 (D)

```
**리뷰 완료** ✅

수고하셨습니다! 문서가 성공적으로 개선되었습니다.

리뷰 히스토리를 저장합니다...
```

Sidecar 파일에 히스토리 저장 후:
```
리뷰 히스토리가 저장되었습니다.

다음에 또 이용해 주세요!
```

워크플로우 종료.

### 5. 추가 수정 선택 (R)

```
추가로 검토할 사항이 있군요.
다시 검토를 시작합니다...
```

→ load, read entire file, then execute {reviewStepFile}

### 6. 새 문서 선택 (N)

```
새 문서 리뷰를 시작합니다.
```

→ 워크플로우를 처음부터 다시 시작 (step-01)

### 7. Sidecar 파일 저장

리뷰 히스토리를 Sidecar 파일에 저장:

**저장 형식:**
```markdown
## [날짜] - [문서 제목]

| 항목 | 내용 |
|------|------|
| URL | [문서 URL] |
| 타입 | [문서 타입] |
| 적용된 개선 | [N]개 |
| 주요 개선 항목 | [요약] |

---
```

**히스토리 관리:**
- 최대 {maxHistoryItems}개 항목 유지
- 초과 시 가장 오래된 항목 삭제
- 최신 항목이 파일 상단에 위치

### 8. 히스토리 정리 (20개 초과 시)

```
리뷰 히스토리 정리 중...
오래된 항목 [N]개가 자동 삭제되었습니다.
```

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- 사용자 확인 후 완료 처리
- Sidecar 파일에 히스토리 정상 저장
- 히스토리 20개 초과 시 자동 정리
- 추가 수정 요청 시 올바르게 step-03으로 돌아감

### ❌ SYSTEM FAILURE:

- 사용자 확인 없이 종료
- 히스토리 저장 실패
- 추가 수정 요청 무시

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.

