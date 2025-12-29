---
name: 'step-03-review'
description: '문서 타입별 기준에 따라 속성, 구조, 내용 검토'

# Path Definitions
workflow_path: '{project-root}/_bmad-output/bmb-creations/workflows/core-platform-notion-reviewer/deployment'

# File References
thisStepFile: '{workflow_path}/steps/step-03-review.md'
nextStepFile: '{workflow_path}/steps/step-04-suggest.md'
workflowFile: '{workflow_path}/workflow.md'

# Data References
documentTypesData: '{workflow_path}/data/document-types.csv'
reviewCriteriaData: '{workflow_path}/data/review-criteria.csv'

# Database IDs
actionItemDbId: '18cce00c-d354-81c7-8930-000b915f03a1'
noteDbId: '879c3173-ae78-4c0d-84b4-6640688ae2f5'
---

# Step 3: 타입별 검토

## STEP GOAL:

확정된 문서 타입에 맞는 기준으로 필수 속성 완성도, Status 규칙(티켓의 경우), 본문 구조/내용, 가독성, 이모지 사용량을 검토합니다.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- ✅ You are a Core Platform Team 문서 품질 전문가
- ✅ 전문성 80%, 친근함 20%의 커뮤니케이션 스타일 유지
- ✅ 근거 기반의 명확한 검토 결과 제공

### Step-Specific Rules:

- 🎯 Focus ONLY on reviewing based on type-specific criteria
- 🚫 FORBIDDEN to suggest improvements in this step (that's step-04)
- 💬 검토 결과를 구조적으로 정리하여 제시

## EXECUTION PROTOCOLS:

- 🎯 문서 타입별 검토 기준 적용
- 💾 발견된 문제점 목록화
- 📖 합리적인 구조면 문제로 표시하지 않음
- 🚫 FORBIDDEN to apply improvements in this step

## CONTEXT BOUNDARIES:

- step-02에서 확정된 문서 타입 사용
- 메모리에 있는 문서 내용과 속성 검토
- 검토만 수행, 개선 제안은 step-04에서

## REVIEW CRITERIA:

### 공통 검토 기준 (모든 문서 타입)

| 기준 | 검토 내용 |
|------|----------|
| **가독성** | 긴 문단 분리, 불렛 포인트/서식 활용 |
| **Notion 스타일** | H1~H3, 인용구, 콜아웃 활용 |
| **이모지 제한** | 전체 텍스트 대비 5% 이내 |
| **표 활용** | 복잡한 구조적 내용에 표 사용 |

### 제안하지 않는 경우

1. 섹션 제목이 다르지만 **동일한 성격의 내용**이 존재
2. IT 기술 조직에서 **합리적인 형태**로 판단되는 경우
3. 가이드라인과 다르지만 **맥락상 적절한 구조**인 경우

## REVIEW SEQUENCE:

### 1. 데이터 파일 로드

{documentTypesData}와 {reviewCriteriaData}를 로드하여 검토 기준을 확인합니다.

### 2. 필수 속성 검토

문서 타입에 따른 필수 속성 완성도를 검토합니다:

**업무 단위 티켓 (action item db):**
- Date: 기간(range) 형태인지 확인
- Person: 담당자가 지정되어 있는지 확인
- Project Name: 프로젝트명이 입력되어 있는지 확인

**그 외 문서 (note db):**
- Tags: 태그가 지정되어 있는지 확인
- Date: 날짜가 입력되어 있는지 확인
- Person: 작성자가 지정되어 있는지 확인

### 3. Status 규칙 검토 (업무 단위 티켓만)

Date 기간과 오늘 날짜를 비교하여 Status 값이 적절한지 검토:

| 오늘 날짜 위치 | 가능한 Status |
|----------------|---------------|
| Date 기간 **전** | 시작 전, Backlog |
| Date 기간 **내** | 검토대기 중, 진행 중, 중단, 완료 |
| Date 기간 **후** | 중단, 완료 |

### 4. 본문 구조 검토

문서 타입별 가이드라인에 따라 본문 구조를 검토합니다.
**주의:** 정확한 섹션 제목이 아니어도 해당 성격의 내용이 있으면 OK

**업무 단위 티켓:**
- Context (배경/맥락)가 충분히 상세한지
- Description (업무 내용)이 충분히 상세한지

**테크스펙:**
- 요약/TL;DR 성격의 내용
- 배경(Background) 성격의 내용
- 목표(Goal) 성격의 내용
- 비목표(Non-Goal) 성격의 내용
- 마일스톤(Milestone) 성격의 내용
- 테스트 계획 성격의 내용

**시스템 소개/기획/설계:**
- Executive Summary 성격의 내용
- 배경(Background) 성격의 내용
- 아키텍처(Architecture) 성격의 내용

**아이데이션/브레인스토밍/기타:**
- 배경(Background) 성격의 내용
- 정리/결론 성격의 내용

### 5. 가독성 및 스타일 검토

- 긴 문단(5줄 이상)이 분리되지 않은 경우
- 불렛 포인트나 서식 부족
- Notion 네이티브 스타일(헤딩, 인용구, 콜아웃) 미활용
- 복잡한 구조적 내용이 줄글로 작성된 경우

### 6. 이모지 사용량 체크

전체 텍스트 대비 이모지 비율 계산:
- 5% 이하: OK
- 5% 초과: 개선 제안 대상

### 7. 논리적 전개 검토

문서 전체를 읽고 제목과 내용의 논리적 연결성을 평가합니다.

**7a. 제목-내용 일치도**
- 문서 제목이 본문의 핵심 내용을 정확히 반영하는가?
- 제목에서 기대되는 내용이 실제로 다뤄지는가?
- 제목과 전혀 무관한 내용이 주를 이루지는 않는가?

**평가 기준:**
| 상태 | 설명 |
|------|------|
| ✅ | 제목이 본문 내용을 잘 대표함 |
| ⚠️ | 제목과 내용이 부분적으로 불일치 |
| ❌ | 제목이 내용을 전혀 반영하지 못함 |

**7b. 논리적 흐름**
- 섹션 순서가 자연스러운가? (일반적: 배경 → 목표 → 내용 → 결론)
- 앞 섹션에서 언급한 내용이 뒤 섹션에서 적절히 이어지는가?
- 갑자기 맥락 없이 등장하는 내용이 없는가?

**7c. 용어/개념 일관성**
- 동일한 개념에 다른 용어를 혼용하지 않는가?
- 정의 없이 갑자기 등장하는 전문 용어나 약어가 없는가?
- 있다면 첫 등장 시 설명이 필요함을 표시

**7d. 줄임말(약어) 감지 및 검토**

문서 내 줄임말을 감지하고 정의 여부를 검토합니다.

**줄임말 감지 패턴:**
- 영문 대문자 2~5자 연속 (예: ODC, PG, MCP)
- 괄호 안 정의가 있는지 확인 (예: "ODC(Open Data Contract)")

**기술조직 공통 줄임말 (정의 불필요):**
다음 줄임말은 기술조직에서 보편적으로 사용되므로 정의 없이 사용 가능:
```
API, DB, SDK, IDE, UI, UX, URL, HTTP, HTTPS, REST, JSON, XML, 
HTML, CSS, JS, TS, SQL, NoSQL, AWS, GCP, K8S, CI, CD, PR, MR,
QA, UAT, SLA, KPI, OKR, ETL, ML, AI, LLM, TDD, BDD, DDD, MVP,
POC, SaaS, PaaS, IaaS, B2B, B2C, CRUD, JWT, OAuth, SSO, RBAC
```

**검토 기준:**
| 상태 | 조건 |
|------|------|
| ✅ 정의됨 | 첫 등장 시 `약어(Full Name)` 형태로 정의됨 |
| ✅ 정의됨 | Glossary/용어집 섹션에 정의됨 |
| ✅ 공통 | 기술조직 공통 줄임말 목록에 포함 |
| ⚠️ 미정의 | 정의 없이 사용됨 → **step-05에서 사용자에게 정의 요청** |

**감지된 줄임말 목록 (미정의만 표시):**
```
| # | 줄임말 | 정의 상태 | 첫 등장 위치 |
|---|--------|----------|-------------|
| 1 | [약어] | ⚠️ 미정의 | [섹션명] |
```

**제안하지 않는 경우:**
- 전체적으로 논리적 흐름이 자연스러운 경우
- 약간의 순서 차이가 있어도 문서 이해에 문제없는 경우
- 해당 문서 타입에서 일반적으로 허용되는 구조인 경우

### 8. Context 미완성 시 관련 문서 검색 (업무 단위 티켓)

Context가 충분하지 않은 경우:
- Notion MCP `notion-search` 또는 `notion-query-data-sources` 사용
- 동일 Project Name 문서 우선 검색
- 최근 문서 우선
- 최대 3~5개 추천

### 9. 검토 결과 정리

검토 결과를 구조적으로 정리:

```
**검토 결과 요약**

| 항목 | 상태 | 비고 |
|------|------|------|
| 필수 속성 | ✅/⚠️/❌ | [세부 내용] |
| Status 규칙 | ✅/⚠️/❌ | [세부 내용] (티켓만) |
| 본문 구조 | ✅/⚠️/❌ | [세부 내용] |
| 가독성 | ✅/⚠️/❌ | [세부 내용] |
| 이모지 | ✅/⚠️/❌ | [비율]% |
| 논리적 전개 | ✅/⚠️/❌ | [제목-내용 일치, 흐름, 일관성] |
| 줄임말 정의 | ✅/⚠️ | [미정의 줄임말 N개] |

발견된 개선 필요 항목: [N]개
미정의 줄임말: [N]개 (사용자 입력 필요)
```

### 10. Auto-Proceed to Next Step

Display: "**검토 완료** - 개선안을 준비합니다..."

#### Menu Handling Logic:

- 검토 완료 후 자동으로 load, read entire file, then execute {nextStepFile}

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- 문서 타입별 기준에 따라 체계적으로 검토
- 합리적인 구조는 문제로 표시하지 않음
- 검토 결과를 구조적으로 정리
- 다음 단계로 자동 진행

### ❌ SYSTEM FAILURE:

- 검토 기준 없이 주관적으로 판단
- 이 단계에서 개선안 제시 또는 적용
- 합리적인 구조를 불필요하게 문제로 표시

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.

