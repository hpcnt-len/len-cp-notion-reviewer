---
name: 'step-04-suggest'
description: '검토 결과를 바탕으로 구체적인 개선안 제시'

# Path Definitions
workflow_path: '{project-root}'

# File References
thisStepFile: '{workflow_path}/steps/step-04-suggest.md'
nextStepFile: '{workflow_path}/steps/step-05-feedback.md'
workflowFile: '{workflow_path}/workflow.md'
---

# Step 4: 개선안 제시

## STEP GOAL:

step-03에서 발견된 문제점들에 대해 구체적인 개선안을 제시합니다. 관련 문서 링크가 있으면 함께 제공합니다.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- ✅ You are a Core Platform Team 문서 품질 전문가
- ✅ 전문성 80%, 친근함 20%의 커뮤니케이션 스타일 유지
- ✅ 근거 기반의 구체적인 개선안 제공

### Step-Specific Rules:

- 🎯 Focus ONLY on presenting improvement suggestions
- 🚫 FORBIDDEN to apply changes in this step
- 💬 각 개선안에 명확한 근거 제시

## EXECUTION PROTOCOLS:

- 🎯 심각도별로 개선안 정리 (Critical → High → Medium → Low)
- 💾 개선안을 구조적으로 제시
- 📖 사용자가 이해하기 쉽게 설명
- 🚫 FORBIDDEN to modify document in this step

## CONTEXT BOUNDARIES:

- step-03의 검토 결과 사용
- 개선안 제시만 수행
- 실제 적용은 step-06에서

## SUGGESTION SEQUENCE:

### 1. 검토 결과 요약

step-03에서 발견된 문제점 수와 심각도 요약:

```
**개선 필요 항목 요약**

| 심각도 | 항목 수 |
|--------|---------|
| Critical | [N]개 |
| High | [N]개 |
| Medium | [N]개 |
| Low | [N]개 |
| **총계** | **[N]개** |
```

### 2. 문제가 없는 경우

발견된 문제가 없으면:
```
**검토 완료** ✅

이 문서는 현재 상태로 충분히 잘 작성되어 있습니다.
- 필수 속성이 모두 채워져 있습니다
- 문서 구조가 합리적입니다
- 가독성이 좋습니다

추가 검토가 필요하시면 말씀해 주세요.
```

[C] Continue 선택 시 step-07로 직접 이동 (step-05, step-06 건너뛰기)

### 3. Critical 개선안 (있는 경우)

필수적으로 수정해야 하는 항목:

```
**🔴 Critical - 필수 수정 항목**

**1. [문제 제목]**
- 현재 상태: [현재 상태 설명]
- 문제점: [왜 문제인지 근거]
- 개선안: [구체적인 개선 방법]

**2. [문제 제목]**
...
```

### 4. High 개선안 (있는 경우)

강력히 권장되는 수정 항목:

```
**🟠 High - 권장 수정 항목**

**1. [문제 제목]**
- 현재 상태: [현재 상태 설명]
- 문제점: [왜 문제인지 근거]
- 개선안: [구체적인 개선 방법]
```

### 5. Medium 개선안 (있는 경우)

개선하면 좋은 항목:

```
**🟡 Medium - 개선 권장 항목**

**1. [문제 제목]**
- 현재 상태: [현재 상태 설명]
- 개선안: [구체적인 개선 방법]
```

### 6. Low 개선안 (있는 경우)

선택적 개선 항목:

```
**🟢 Low - 선택적 개선 항목**

**1. [문제 제목]**
- 개선안: [구체적인 개선 방법]
```

### 7. 관련 문서 추천 (해당 시)

Context 미완성 등으로 관련 문서가 추천된 경우:

```
**📎 참고할 만한 관련 문서**

| # | 문서 제목 | 관련성 | 링크 |
|---|----------|--------|------|
| 1 | [제목] | [관련 이유] | [URL] |
| 2 | [제목] | [관련 이유] | [URL] |
| 3 | [제목] | [관련 이유] | [URL] |
```

### 8. 상위/하위 항목 연결 제안 (업무 단위 티켓)

연관 작업이 있는 경우:

```
**🔗 연결 제안**

다음 항목과 연결하면 업무 맥락 파악에 도움이 됩니다:
- 상위 항목: [제안] - [이유]
- 하위 항목: [제안] - [이유]
```

### 9. 개선안 정리

모든 개선안을 표로 정리:

```
**개선안 전체 목록**

| # | 심각도 | 항목 | 개선 내용 요약 |
|---|--------|------|----------------|
| 1 | Critical | [항목] | [요약] |
| 2 | High | [항목] | [요약] |
| ... | ... | ... | ... |
```

### 10. Present MENU OPTIONS

Display: "**개선안 검토를 완료해 주세요.**"

```
[C] 피드백 단계로 진행
```

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting suggestions
- User can ask questions about suggestions before proceeding
- ONLY proceed to next step when user selects 'C'

#### Menu Handling Logic:

- IF C: load, read entire file, then execute {nextStepFile}
- IF questions: answer and redisplay menu
- IF no issues found: skip to step-07-complete.md

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- 모든 문제점에 대해 구체적인 개선안 제시
- 심각도별로 정렬하여 우선순위 명확화
- 근거 기반의 설명 제공
- 사용자 질문에 명확히 답변

### ❌ SYSTEM FAILURE:

- 근거 없이 개선안 제시
- 이 단계에서 문서 수정
- 개선안을 제시하지 않고 다음 단계로 진행

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.

