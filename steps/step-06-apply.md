---
name: 'step-06-apply'
description: 'Notion MCP를 사용하여 승인된 개선안을 문서에 적용'

# Path Definitions
workflow_path: '{project-root}'

# File References
thisStepFile: '{workflow_path}/steps/step-06-apply.md'
nextStepFile: '{workflow_path}/steps/step-07-complete.md'
workflowFile: '{workflow_path}/workflow.md'
---

# Step 6: Notion 문서 업데이트

## STEP GOAL:

step-05에서 승인된 개선안을 Notion MCP를 사용하여 실제 문서에 적용합니다.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- ✅ You are a Core Platform Team 문서 품질 전문가
- ✅ 전문성 80%, 친근함 20%의 커뮤니케이션 스타일 유지
- ✅ 신중하고 안전하게 문서 수정

### Step-Specific Rules:

- 🎯 Focus ONLY on applying approved changes via Notion MCP
- 🚫 FORBIDDEN to modify content beyond approved changes
- ⚠️ 이미지, 임베드 등 기존 미디어 블록은 건드리지 않음
- 💬 적용 진행 상황을 명확히 안내

## EXECUTION PROTOCOLS:

- 🎯 승인된 항목만 정확히 적용
- 💾 적용 결과 기록
- 📖 에러 발생 시 복구 옵션 제공
- 🚫 FORBIDDEN to apply non-approved changes

## CONTEXT BOUNDARIES:

- step-05에서 승인된 개선안 목록 사용
- Notion MCP notion-update-page로 적용
- 미디어 블록(이미지, 임베드 등) 보호

## APPLY SEQUENCE:

### 1. 변경 내용 미리보기 생성

승인된 각 개선안에 대해 **실제 적용될 내용**을 구체적으로 생성합니다:

**속성 변경의 경우:**
- 현재 값과 변경될 값을 명시

**본문 변경의 경우:**
- 추가/수정될 실제 텍스트를 Notion Markdown 형식으로 생성
- 문서의 맥락과 스타일에 맞게 작성

### 2. 변경 내용 미리보기 표시 (사용자 확인 필수)

```
**📝 변경 내용 미리보기**

다음 내용이 Notion 문서에 적용됩니다:

---

**[1] [항목명]**

📍 **위치:** [어디에 추가/수정되는지]

**추가될 내용:**
```markdown
[실제 추가될 Notion Markdown 내용을 여기에 표시]
```

---

**[2] [항목명]** (있는 경우)
...

---

⚠️ 이미지, 임베드 등 미디어 블록은 변경되지 않습니다.

[Y] 이대로 적용 [M] 내용 수정 요청 [Q] 적용 취소
```

### 3. 사용자 확인 처리

#### [Y] 이대로 적용
미리보기 내용 그대로 Notion에 적용 진행

#### [M] 내용 수정 요청
```
어떤 부분을 수정할까요?
(예: "배경 설명을 더 간결하게", "다른 표현으로 변경" 등)
```
사용자 피드백을 반영하여 미리보기 재생성 → 다시 확인

#### [Q] 적용 취소
적용하지 않고 step-07로 이동 (개선 0개로 기록)

### 4. 속성 수정 적용 (해당 시)

Notion MCP `notion-update-page`를 사용하여 속성 수정:

```
**속성 수정 중...**

[1/N] Date 속성 수정... ✅
[2/N] Person 속성 수정... ✅
...
```

### 5. 본문 수정 적용

Notion MCP `notion-update-page`를 사용하여 본문 수정:

**주의사항:**
- 이미지, 임베드, 데이터베이스 뷰 등 미디어 블록은 건드리지 않음
- 텍스트 블록만 수정
- 기존 구조 최대한 유지

**⚠️ Table of Contents (TOC) 추가 시 주의:**
Notion의 TOC 블록은 API로 직접 생성할 수 없습니다.
TOC 추가가 승인된 경우, 아래와 같이 **수동 추가 안내**를 제공합니다:

```
**📋 Table of Contents 수동 추가 안내**

Notion의 목차(TOC) 블록은 API로 직접 추가할 수 없어 수동 추가가 필요합니다.

**추가 방법:**
1. Notion에서 해당 문서를 엽니다
2. 목차를 추가할 위치 (보통 문서 최상단)에 커서를 놓습니다
3. `/toc` 입력 후 "Table of Contents" 선택

**권장 위치:** 문서 제목 바로 아래, 첫 번째 섹션 위

[C] 완료 후 계속
```

```
**본문 수정 중...**

[1/N] [섹션명] 수정... ✅
[2/N] [섹션명] 추가... ✅
...
```

### 6. 에러 처리

적용 중 에러 발생 시:

```
**⚠️ 적용 중 오류 발생**

오류 내용: [에러 메시지]
실패한 항목: [항목명]

[R] 재시도
[M] 수동 적용 안내 (변경 내용을 클립보드에 복사)
[S] 이 항목 건너뛰고 계속
```

#### [R] 재시도
해당 항목만 다시 적용 시도

#### [M] 수동 적용 안내
```
**수동 적용 안내**

다음 내용을 Notion에서 직접 수정해 주세요:

**수정할 위치:** [위치 설명]
**변경 내용:**
```
[변경할 내용을 코드 블록으로 표시]
```

위 내용이 클립보드에 복사되었습니다.
Notion에서 해당 위치에 붙여넣기 해주세요.

[C] 계속 진행
```

#### [S] 건너뛰기
해당 항목을 건너뛰고 다음 항목 적용

### 7. 적용 결과 요약

모든 적용 완료 후:

```
**적용 완료** ✅

| 결과 | 항목 수 |
|------|---------|
| 성공 | [N]개 |
| 건너뜀 | [N]개 |
| 수동 적용 필요 | [N]개 |

문서가 성공적으로 업데이트되었습니다.
```

### 8. Auto-Proceed to Next Step

Display: "**완료 확인 단계로 진행합니다...**"

#### Menu Handling Logic:

- 적용 완료 후 자동으로 load, read entire file, then execute {nextStepFile}

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- 승인된 항목만 정확히 적용
- 미디어 블록 보호됨
- 에러 발생 시 적절한 복구 옵션 제공
- 적용 결과 명확히 요약

### ❌ SYSTEM FAILURE:

- 승인되지 않은 변경 적용
- 미디어 블록 손상
- 에러 무시하고 진행
- 적용 결과 보고 누락

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.

