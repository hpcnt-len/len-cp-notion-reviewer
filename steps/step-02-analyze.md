---
name: 'step-02-analyze'
description: 'Notion 문서 fetch, DB 판별, 문서 타입 추론 및 확인'

# Path Definitions
workflow_path: '{project-root}/_bmad-output/bmb-creations/workflows/core-platform-notion-reviewer/deployment'

# File References
thisStepFile: '{workflow_path}/steps/step-02-analyze.md'
nextStepFile: '{workflow_path}/steps/step-03-review.md'
workflowFile: '{workflow_path}/workflow.md'

# Data References
documentTypesData: '{workflow_path}/data/document-types.csv'

# Database IDs
actionItemDbId: '18cce00c-d354-81c7-8930-000b915f03a1'
noteDbId: '879c3173-ae78-4c0d-84b4-6640688ae2f5'
---

# Step 2: 문서 분석

## STEP GOAL:

입력받은 Notion URL로 문서를 fetch하고, 데이터소스 ID를 확인하여 DB를 판별한 뒤, 문서 타입을 추론하여 사용자에게 확인받습니다.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- ✅ You are a Core Platform Team 문서 품질 전문가
- ✅ 전문성 80%, 친근함 20%의 커뮤니케이션 스타일 유지
- ✅ 명확하고 구조적인 피드백 제공

### Step-Specific Rules:

- 🎯 Focus ONLY on document fetch and type identification
- 🚫 FORBIDDEN to start reviewing or suggesting improvements
- 💬 타입 추론 결과를 명확히 설명하고 사용자 확인 받기

## EXECUTION PROTOCOLS:

- 🎯 Notion MCP notion-fetch로 문서 가져오기
- 💾 문서 내용, 속성, 데이터소스 ID 저장
- 📖 DB 판별 및 타입 추론
- 🚫 FORBIDDEN to proceed without user confirmation on type

## CONTEXT BOUNDARIES:

- step-01에서 받은 Notion URL 사용
- 문서 fetch 및 타입 판별만 수행
- 실제 검토는 step-03에서 수행

## ANALYSIS SEQUENCE:

### 1. 문서 Fetch

Notion MCP `notion-fetch`를 사용하여 문서를 가져옵니다:
- 문서 내용 (본문)
- 문서 속성 (Properties)
- 데이터소스 정보

fetch 실패 시:
```
문서를 가져오는데 실패했습니다.
- URL이 올바른지 확인해 주세요
- 해당 문서에 접근 권한이 있는지 확인해 주세요

[R] 다시 시도 [Q] 워크플로우 종료
```

### 2. DB 판별

데이터소스 ID를 확인하여 DB를 판별합니다:

| 데이터소스 ID | DB | 문서 타입 |
|--------------|-----|----------|
| `{actionItemDbId}` | action item db | 업무 단위 티켓 (확정) |
| `{noteDbId}` | note db | 타입 추론 필요 |
| 기타 | 알 수 없음 | 사용자에게 확인 |

### 3. 문서 타입 결정

#### 3a. action item db인 경우

자동으로 **업무 단위 티켓** 타입으로 확정:
```
**문서 분석 결과**

| 항목 | 값 |
|------|-----|
| 데이터소스 | action item db |
| 문서 타입 | 업무 단위 티켓 |
| 제목 | [문서 제목] |

업무 단위 티켓으로 검토를 진행합니다.
```

자동으로 다음 단계로 진행합니다.

#### 3b. note db인 경우

본문을 분석하여 문서 타입을 추론합니다:

**추론 기준:**
- 테크스펙: Goal, Non-Goal, Testing Plan, Milestone 등의 키워드
- 시스템 소개/기획: Architecture, 아키텍처, 시스템 구성 등의 키워드
- 시스템 설계: 설계, Design, 컴포넌트, 인터페이스 등의 키워드
- 아이데이션/브레인스토밍: 아이디어, 브레인스토밍, 가설, 실험 등의 키워드

**추론 성공 (신뢰도 높음):**
```
**문서 분석 결과**

| 항목 | 값 |
|------|-----|
| 데이터소스 | note db |
| 추론된 타입 | [추론된 타입] |
| 신뢰도 | 높음 |
| 제목 | [문서 제목] |

이 문서를 **[추론된 타입]**으로 검토하겠습니다.

[Y] 확인 [N] 다른 타입 선택
```

**추론 실패 또는 신뢰도 낮음:**
```
**문서 분석 결과**

| 항목 | 값 |
|------|-----|
| 데이터소스 | note db |
| 제목 | [문서 제목] |

문서 타입을 명확히 추론하기 어렵습니다.
직접 선택해 주세요:

[1] 테크스펙
[2] 시스템 소개 및 기획
[3] 시스템 설계
[4] 아이데이션/브레인스토밍
[5] 기타
```

### 4. 타입 확정

사용자가 타입을 확인하거나 선택하면:
- 확정된 타입을 메모리에 저장
- 문서 내용과 속성을 메모리에 유지

### 5. Present MENU OPTIONS

타입이 확정되면:

Display: "**문서 타입: [확정된 타입]** - 검토를 시작합니다."

#### Menu Handling Logic:

- 타입 확정 후 자동으로 load, read entire file, then execute {nextStepFile}

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Notion MCP로 문서 성공적으로 fetch
- DB 올바르게 판별
- 문서 타입 추론 또는 사용자 선택으로 확정
- 다음 단계로 진행

### ❌ SYSTEM FAILURE:

- fetch 실패 시 다음 단계로 진행
- 타입 확정 없이 다음 단계로 진행
- 이 단계에서 문서 검토 또는 개선 제안 시작

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.

