---
name: 'step-01-init'
description: 'Notion URL 입력 받기 및 Sidecar 파일 로드'

# Path Definitions
workflow_path: '{project-root}'

# File References
thisStepFile: '{workflow_path}/steps/step-01-init.md'
nextStepFile: '{workflow_path}/steps/step-02-analyze.md'
workflowFile: '{workflow_path}/workflow.md'

# Data References
documentTypesData: '{workflow_path}/data/document-types.csv'
reviewCriteriaData: '{workflow_path}/data/review-criteria.csv'

# Sidecar File
sidecarFile: '{workflow_path}/sidecar/review-history.md'

# Database IDs
actionItemDbId: '18cce00c-d354-81c7-8930-000b915f03a1'
noteDbId: '879c3173-ae78-4c0d-84b4-6640688ae2f5'
---

# Step 1: 초기화

## STEP GOAL:

사용자로부터 리뷰할 Notion 문서의 URL을 입력받고, 이전 리뷰 히스토리(Sidecar 파일)를 로드하여 워크플로우를 시작할 준비를 합니다.

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
- ✅ 근거 기반 제안

### Step-Specific Rules:

- 🎯 Focus ONLY on URL 입력 받기 and Sidecar 로드
- 🚫 FORBIDDEN to start document analysis in this step
- 💬 간결하고 명확한 안내 제공

## EXECUTION PROTOCOLS:

- 🎯 Notion URL 유효성 간단히 확인 (notion.so 도메인)
- 💾 Sidecar 파일이 있으면 로드하여 이전 히스토리 확인
- 📖 URL 입력 후 자동으로 다음 단계로 진행
- 🚫 FORBIDDEN to analyze document content in this step

## CONTEXT BOUNDARIES:

- 이 단계에서는 URL 입력만 받습니다
- 문서 분석은 step-02에서 수행합니다
- Sidecar 파일은 참조용으로만 로드합니다

## INITIALIZATION SEQUENCE:

### 1. 환영 메시지

Display:
```
**Core Platform Notion Reviewer**

Notion 문서의 품질을 검토하고 개선안을 제안합니다.

리뷰할 Notion 문서의 URL을 입력해 주세요.
(예: https://www.notion.so/your-workspace/document-id)
```

### 2. Sidecar 파일 확인

Sidecar 파일({sidecarFile})이 존재하는지 확인합니다:
- 존재하면: 이전 리뷰 히스토리를 참조용으로 메모리에 로드
- 존재하지 않으면: 새 세션으로 진행 (파일은 step-07에서 생성)

### 3. URL 입력 대기

사용자가 Notion URL을 입력할 때까지 대기합니다.

입력된 URL 검증:
- notion.so 또는 notion.site 도메인 포함 여부
- URL 형식이 올바른지 확인

유효하지 않은 URL인 경우:
```
입력하신 URL이 Notion 문서 URL이 아닌 것 같습니다.
notion.so 또는 notion.site 도메인의 URL을 입력해 주세요.
```

### 4. 다음 단계로 진행

유효한 URL이 입력되면:
```
URL을 확인했습니다. 문서를 분석합니다...
```

URL을 메모리에 저장하고, 자동으로 다음 단계로 진행합니다.

### 5. Auto-Proceed to Next Step

Display: "**문서 분석을 시작합니다...**"

#### Menu Handling Logic:

- URL 입력 완료 후 자동으로 load, read entire file, then execute {nextStepFile}

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- 유효한 Notion URL 입력 받음
- Sidecar 파일 로드 시도 (있으면 로드, 없으면 스킵)
- URL을 메모리에 저장
- 다음 단계로 자동 진행

### ❌ SYSTEM FAILURE:

- URL 없이 다음 단계로 진행
- 문서 분석을 이 단계에서 시작
- 잘못된 URL을 수락

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.

