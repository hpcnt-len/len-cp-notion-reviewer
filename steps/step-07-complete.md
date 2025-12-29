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
| 톤 통일 (존댓말) | ✅ / ⚠️ |
| 수동 프로세스 | ✅ 없음 / ⚠️ 대기 중 [N]개 |
```

### 3. 완료 확인 메뉴

```
**다음 중 선택해 주세요:**

[D] 완료 - 리뷰를 마칩니다
[R] 추가 수정 - 다시 검토합니다
[N] 새 문서 - 다른 문서를 리뷰합니다
```

### 4. 완료 선택 (D) - 수동 프로세스 검증 포함

#### 4a. 원격 문서 재로드

```
**최종 검증 중...**

수동 프로세스 반영 여부를 확인하기 위해 문서를 다시 불러옵니다...
```

Notion MCP `notion-fetch`를 사용하여 원격 문서를 다시 로드합니다.

#### 4b. 수동 프로세스 반영 확인

**수동 추가 안내가 있었던 항목:**
- Table of Contents (TOC) 추가
- 기타 API로 추가 불가능했던 항목

**검증 방법:**
1. 문서 본문에서 TOC 블록 존재 여부 확인
2. 안내되었던 수동 항목들이 실제로 반영되었는지 체크

**검증 결과 표시:**

```
**수동 프로세스 검증 결과**

| 항목 | 상태 | 비고 |
|------|------|------|
| Table of Contents | ✅ 확인됨 / ⚠️ 미반영 | [상세] |
| [기타 수동 항목] | ✅ 확인됨 / ⚠️ 미반영 | [상세] |
```

#### 4c. 미반영 항목이 있는 경우

```
**⚠️ 수동 반영이 필요한 항목이 있습니다**

다음 항목이 아직 반영되지 않았습니다:
- [미반영 항목 목록]

[P] 지금 반영 (안내 다시 표시)
[S] 건너뛰고 완료
```

**[P] 선택 시:**
해당 수동 프로세스 안내를 다시 표시하고, 사용자가 완료한 후 다시 검증

**[S] 선택 시:**
미반영 상태로 완료 처리 (히스토리에 미반영 항목 기록)

#### 4d. 모든 항목 반영 완료 시

```
**리뷰 완료** ✅

모든 개선 사항이 성공적으로 반영되었습니다!

리뷰 히스토리를 저장합니다...
```

Sidecar 파일에 히스토리 저장 후:
```
리뷰 히스토리가 저장되었습니다.

수고하셨습니다! 다음에 또 이용해 주세요!
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
| 수동 프로세스 | ✅ 완료 / ⚠️ 미반영 [항목명] |

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

