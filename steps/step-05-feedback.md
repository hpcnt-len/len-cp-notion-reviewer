---
name: 'step-05-feedback'
description: '사용자 피드백 수집 - 승인, 수정 요청, 부분 승인'

# Path Definitions
workflow_path: '{project-root}/_bmad-output/bmb-creations/workflows/core-platform-notion-reviewer/deployment'

# File References
thisStepFile: '{workflow_path}/steps/step-05-feedback.md'
nextStepApply: '{workflow_path}/steps/step-06-apply.md'
prevStepSuggest: '{workflow_path}/steps/step-04-suggest.md'
workflowFile: '{workflow_path}/workflow.md'
---

# Step 5: 사용자 피드백

## STEP GOAL:

제시된 개선안에 대해 사용자의 피드백을 수집합니다. 전체 승인, 수정 요청, 또는 부분 승인을 처리합니다.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- ✅ You are a Core Platform Team 문서 품질 전문가
- ✅ 전문성 80%, 친근함 20%의 커뮤니케이션 스타일 유지
- ✅ 사용자 피드백을 존중하며 유연하게 대응

### Step-Specific Rules:

- 🎯 Focus ONLY on collecting and processing user feedback
- 🚫 FORBIDDEN to apply changes without explicit approval
- 💬 사용자 의견을 명확히 이해하고 반영

## EXECUTION PROTOCOLS:

- 🎯 피드백 옵션을 명확히 제시
- 💾 승인된 개선안 목록 저장
- 📖 수정 요청 시 step-04로 돌아가 재제안
- 🚫 FORBIDDEN to proceed without clear user decision

## CONTEXT BOUNDARIES:

- step-04에서 제시된 개선안 참조
- 피드백 수집만 수행
- 실제 적용은 step-06에서

## FEEDBACK SEQUENCE:

### 1. 피드백 옵션 제시

```
**개선안 피드백**

제시된 개선안에 대해 선택해 주세요:

[A] 전체 승인 - 모든 개선안을 적용합니다
[P] 부분 승인 - 적용할 항목을 선택합니다
[M] 수정 요청 - 개선안 수정을 요청합니다
[Q] 취소 - 개선 없이 종료합니다
```

### 2. 전체 승인 (A)

사용자가 [A]를 선택한 경우:

```
**전체 승인 확인**

다음 개선안을 모두 적용합니다:

| # | 항목 | 개선 내용 |
|---|------|----------|
| 1 | [항목] | [내용] |
| 2 | [항목] | [내용] |
...

총 [N]개 항목이 적용됩니다.

[Y] 확인하고 적용 진행 [N] 다시 선택
```

### 3. 부분 승인 (P)

사용자가 [P]를 선택한 경우:

```
**부분 승인 - 적용할 항목 선택**

적용할 항목의 번호를 입력해 주세요. (쉼표로 구분)
예: 1, 3, 5

| # | 심각도 | 항목 | 개선 내용 |
|---|--------|------|----------|
| 1 | Critical | [항목] | [내용] |
| 2 | High | [항목] | [내용] |
| 3 | Medium | [항목] | [내용] |
...

선택: 
```

선택 후:
```
**선택된 항목 확인**

다음 항목만 적용합니다:
- [선택된 항목 1]
- [선택된 항목 2]
...

[Y] 확인하고 적용 진행 [N] 다시 선택
```

### 4. 수정 요청 (M)

사용자가 [M]을 선택한 경우:

```
**수정 요청**

어떤 부분을 수정해 드릴까요?

1. 특정 개선안의 내용 변경
2. 개선안 삭제
3. 새로운 개선 방향 제안
4. 기타

원하시는 수정 사항을 설명해 주세요:
```

수정 요청 내용을 받은 후:
- 피드백 내용을 메모리에 저장
- step-04로 돌아가 수정된 개선안 재제안

```
수정 요청을 반영하여 개선안을 다시 준비합니다...
```

→ load, read entire file, then execute {prevStepSuggest}

### 5. 취소 (Q)

사용자가 [Q]를 선택한 경우:

```
**개선 취소 확인**

개선 없이 워크플로우를 종료하시겠습니까?

[Y] 예, 종료합니다 [N] 아니오, 계속합니다
```

### 6. 미정의 줄임말 정의 요청 (해당 시)

step-03에서 미정의 줄임말이 감지된 경우, 승인 전에 사용자에게 정의를 요청합니다.

```
**📝 줄임말 정의 필요**

다음 줄임말의 Full Description을 입력해 주세요.
(기술조직 공통 줄임말은 이미 제외되었습니다)

| # | 줄임말 | 첫 등장 위치 |
|---|--------|-------------|
| 1 | [약어1] | [섹션명] |
| 2 | [약어2] | [섹션명] |

**입력 형식:** `줄임말: Full Description`
예: `ODC: Open Data Contract`

여러 개인 경우 줄바꿈으로 구분:
```
ODC: Open Data Contract
PG: Payment Gateway
```

입력해 주세요 (완료 시 'done' 입력):
```

**사용자 입력 처리:**
1. 각 줄임말에 대한 Full Description을 메모리에 저장
2. 문서에 적용할 방식 선택 요청:

```
**줄임말 표기 방식 선택**

입력하신 정의를 문서에 어떻게 적용할까요?

[1] 첫 등장 시 인라인 정의
    예: "ODC(Open Data Contract) 프레임워크를 사용합니다"
    
[2] Glossary 섹션 추가
    문서 하단에 용어집 섹션을 추가합니다
    
[3] 둘 다 적용
    첫 등장 시 인라인 + Glossary 섹션

선택:
```

**저장 형식:**
```
abbreviations:
  - abbr: "ODC"
    full: "Open Data Contract"
    location: "1. 개요"
    apply_method: "inline" | "glossary" | "both"
```

### 7. 승인 완료

전체 승인 또는 부분 승인이 확정되면:

```
**승인 완료** ✅

[N]개 항목이 승인되었습니다.
[M]개 줄임말 정의가 추가됩니다.
Notion 문서에 적용을 시작합니다.
```

### 8. Present MENU OPTIONS

승인 완료 후:

Display: "**적용 단계로 진행합니다...**"

#### Menu Handling Logic:

- IF A (전체 승인) confirmed: 
  - 미정의 줄임말 있으면 → 6번(줄임말 정의 요청) 실행 후 → load {nextStepApply}
  - 없으면 → load {nextStepApply}
- IF P (부분 승인) confirmed: 
  - 미정의 줄임말 있으면 → 6번(줄임말 정의 요청) 실행 후 → load {nextStepApply}
  - 없으면 → load {nextStepApply}
- IF M (수정 요청): save feedback, load {prevStepSuggest} (반복)
- IF Q (취소) confirmed: skip to step-07-complete.md with no changes

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- 사용자 피드백 명확히 수집
- 승인된 항목 정확히 저장
- 수정 요청 시 올바르게 step-04로 돌아감
- 명확한 확인 후 다음 단계로 진행

### ❌ SYSTEM FAILURE:

- 사용자 확인 없이 승인 처리
- 수정 요청을 무시하고 진행
- 승인된 항목을 누락

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.

