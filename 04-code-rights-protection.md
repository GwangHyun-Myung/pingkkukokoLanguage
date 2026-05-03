---
date: 2026-05-03
type: legal-policy
step: 4
related: [[01-license-audit]], [[02-license-compatibility]], [[03-distribution-structure]], [[05-proprietary-license]]
---

# 04 — 자체 코드의 권리 보호 (Code Rights Protection)

> **면책 고지**: 이 문서는 프로젝트 내부 참고용 자료이며 법적 조언(legal advice)이 아닙니다. 저작권 보호 및 라이선스 집행 전략에 관한 최종 판단은 반드시 자격을 갖춘 변호사(attorney)에게 검토를 의뢰하십시오.

---

## 1. 개요

이 문서는 pingkkukoko의 자체 코드(original code)와 UI 자산(UI assets)에 대한 저작권 보호 방법을 정의합니다. CC 라이선스 데이터와 독점 코드 간의 경계를 명확히 하고, 향후 오픈소스 기여나 저작권 분쟁 발생 시 대응 절차를 기록합니다.

---

## 2. 저작권 고지 헤더 (Copyright Notice Headers)

### 2.1 헤더 포함 여부 결정

소스 파일 상단에 저작권 고지(copyright notice)를 삽입하는 관행에는 장단점이 있습니다.

| 장점 | 단점 |
|------|------|
| 저작권 귀속(attribution) 명시 → 법적 보호 강화 | 모든 파일에 반복되는 보일러플레이트(boilerplate) → 코드 가독성 저하 |
| 소스가 외부로 유출되어도 출처 식별 가능 | 파일 생성 날짜마다 연도 업데이트 관리 부담 |
| 오픈소스 라이선스와의 혼용 시 명확한 경계 설정 | IDE에서 파일 상단이 코드 내용이 아닌 주석으로 시작 |

**권장 (Recommended)**: 대부분의 소규모 독점 앱은 루트 `LICENSE` 파일만으로도 저작권을 충분히 보호할 수 있습니다. 그러나 데이터 레이어(`datas/`)와 코드 레이어(`apps/src/`, `tools/src/`)가 혼재하는 이 프로젝트에서는 **코드 파일 상단에 간략한 1-2행 헤더를 추가**하는 것이 경계를 명확히 하는 데 효과적입니다.

### 2.2 권장 저작권 헤더 템플릿

**영문 (English)**
```typescript
// Copyright (c) <YEAR> <COPYRIGHT_HOLDER>. All Rights Reserved.
// Proprietary and confidential. Unauthorized copying or distribution is prohibited.
```

**한국어 병기 버전 (Korean + English)**
```typescript
// Copyright (c) <YEAR> <COPYRIGHT_HOLDER>. All Rights Reserved.
// 이 파일은 저작권자의 독점 소유입니다. 무단 복사·배포·변형을 금합니다.
```

**적용 대상**
- `apps/src/**/*.ts`
- `apps/src/**/*.tsx`
- `tools/**/*.ts`

**적용 제외 대상**
- `apps/src/data/<lang>/*.json` — CC-BY-SA 파생 데이터이므로 독점 헤더 부적합
- 자동 생성 파일(generated files) — 빌드 도구가 덮어씀
- `node_modules/` 내 파일 — 외부 패키지

> **검토 필요**: `<YEAR>`는 파일 최초 생성 연도를 기준으로 하거나, 현재 연도와 최초 생성 연도를 "2025–2026" 형식으로 병기하는 방식을 사용합니다. `<COPYRIGHT_HOLDER>`는 개인 이름, 법인명, 또는 브랜드명 중 법적으로 유효한 주체로 기재합니다.

---

## 3. 원본 콘텐츠 경계 (Original Content Boundary)

저작권 보호 범위를 명확히 하기 위해 "자체 원본 콘텐츠(original content)"와 "파생 데이터(derived data)"의 경계를 정의합니다.

### 3.1 독점 소유물 — 자체 원본 콘텐츠

| 구성 요소 | 경로 | 성격 |
|----------|------|------|
| 앱 아키텍처 및 레이어 구조 | `apps/src/` 전체 | 독점 저작물 |
| 게이미피케이션 로직 (XP, 레벨, 연속 학습) | `apps/src/services/GamificationService.ts` 등 | 독점 저작물 |
| SRS 스케줄링 통합 코드 | `apps/src/services/ExerciseService.ts` 등 | 독점 저작물 |
| SQLite 저장소 레이어 | `apps/src/database/` | 독점 저작물 |
| Zustand 스토어 | `apps/src/store/` | 독점 저작물 |
| UI 컴포넌트 및 화면 | `apps/src/components/`, `apps/app/` | 독점 저작물 |
| 게이미피케이션 상수 (XP 공식, 레벨 임계값) | `apps/src/constants/gamification.ts` | 독점 저작물 |
| 앱 스키마 (JSON 데이터 구조 정의) | 스키마 타입 정의 파일 | 독점 저작물 |
| 파이프라인 소스 코드 | `tools/data-pipeline/src/` | 독점 저작물 |
| UI 자산 (아이콘, 애니메이션, 마스코트) | `apps/assets/` | 독점 저작물 |
| 빌드 설정 (EAS, expo 설정) | `apps/app.json`, `apps/eas.json` 등 | 독점 저작물 |

### 3.2 CC 라이선스 파생물 — 외부 소스에서 파생

| 구성 요소 | 경로 | 적용 라이선스 |
|----------|------|-------------|
| 언어별 번들 코어 데이터 | `apps/src/data/<lang>/unit*.json` | CC-BY-SA 4.0 |
| 전체 콘텐츠 청크 아카이브 | `datas/content-v1/*.jsonl.gz` | CC-BY-SA 4.0 |

> **중요**: `apps/src/data/<lang>/unit*.json` 파일에는 독점 저작권 헤더를 추가하지 않습니다. 이 파일들은 CC-BY-SA 소스에서 파생되었으므로, 독점 라이선스 헤더를 삽입하면 CC 라이선스 의무를 위반하게 됩니다.

---

## 4. 외부 기여 정책 (CONTRIBUTING / CLA)

프로젝트가 공개(public) 저장소로 전환되거나, 외부 기여자(contributor)를 받아들이는 경우의 권장 정책입니다.

### 4.1 CLA (Contributor License Agreement) 방식

**권장 대상**: 상업적 배포를 유지하면서 외부 기여를 받는 경우.

CLA는 기여자가 기여물(contribution)에 대한 권리를 프로젝트 소유자에게 부여하는 법적 동의서입니다. 기여자는 자신의 기여물에 대한 저작권을 유지하면서, 프로젝트 소유자에게 해당 기여물을 독점 라이선스 하에 포함시킬 수 있는 권한을 부여합니다.

구현 방법:
- GitHub의 `cla-assistant` 또는 `contributor-assistant` 봇 사용
- PR 제출 시 CLA 서명 자동 요청
- 법인 기여자(corporate contributor)를 위한 별도 CLA 문서 준비

### 4.2 DCO (Developer Certificate of Origin) 방식

**권장 대상**: CLA 행정 부담을 줄이되 기여물의 적법성을 보장하고 싶은 경우.

DCO는 기여자가 자신의 기여물이 적법하게 제출되었음을 인증하는 가벼운 메커니즘입니다. 기여자는 각 커밋에 다음 서명을 추가합니다.

```
Signed-off-by: Jane Doe <jane@example.com>
```

Linux 커널, Docker 등의 프로젝트가 DCO를 사용합니다.

### 4.3 현 단계 (비공개 저장소) 권장 사항

현재 프로젝트가 비공개 또는 소수 기여자 환경이라면, 공식 CLA/DCO 도입 전 다음을 `CONTRIBUTING.md`에 명시하는 것으로 충분합니다.

```markdown
## 기여 정책

이 저장소에 코드를 기여하면, 귀하는 해당 기여물에 대해 프로젝트 소유자 <COPYRIGHT_HOLDER>에게 
비독점적, 영구적, 전 세계적, 로열티-무료 라이선스를 부여하는 것에 동의하는 것으로 간주됩니다.
기여물이 CC 라이선스 데이터 레이어에 관한 것이라면, CC-BY-SA 4.0 조건이 별도로 적용됩니다.
```

---

## 5. 트레이드마크 및 브랜드 보호 (Trademark and Brand)

### 5.1 pingkkukoko 명칭

"pingkkukoko" 이름과 관련 마스코트 캐릭터는 프로젝트 소유자의 고유 브랜드 자산(brand asset)입니다. 저작권(copyright)과 트레이드마크(trademark)는 별개의 법적 보호 체계입니다.

| 보호 유형 | 대상 | 법적 근거 |
|----------|------|---------|
| 저작권 (Copyright) | 소스 코드, UI 디자인, 마스코트 일러스트 | 창작 즉시 자동 발생 |
| 트레이드마크 (Trademark) | "pingkkukoko" 명칭, 로고, 마스코트 스타일 | 사용 기반 권리 (common law); 등록 시 강화 |

**권장 사항**
- 앱 설명, 스토어 페이지, 마케팅 자료에 ™ 또는 ® 기호 사용
- 한국 특허청(KIPO) 및 필요 시 미국 USPTO에 트레이드마크 등록 검토
- CC 라이선스는 앱 데이터에만 적용되며, pingkkukoko 브랜드 명칭에는 적용되지 않음을 명시

> **검토 필요**: CC-BY-SA 라이선스 하의 데이터를 재배포하는 제3자가 pingkkukoko 브랜드를 함께 사용하는 것을 방지하기 위해, 데이터 배포 시 "pingkkukoko 브랜드 및 마스코트 사용은 별도 허가가 필요합니다"라는 문구를 ATTRIBUTIONS.txt에 포함하는 것을 권장합니다.

---

## 6. DMCA / 저작권 침해 신고 대응 절차 (DMCA Takedown Response Process)

CC 라이선스 원천 소스의 업스트림 권리 보유자가 pingkkukoko의 파생 데이터에 대해 침해 신고(takedown notice)를 제출하는 경우를 대비한 기술적·행정적 절차를 정의합니다.

### 6.1 신고 접수 시 즉각 조치

**신고 접수 이메일**: prozect@hanmail.net

1. **24시간 이내**: 해당 소스 데이터의 사용을 일시 중단(suspend)하고, 침해 주장 범위를 확인
2. **72시간 이내**: 법률 자문 요청 및 침해 주장의 유효성 검토
3. **유효 신고 확인 시**: 아래 기술적 절차 실행

### 6.2 기술적 대응 절차

파이프라인은 소스별 데이터를 분리 추적할 수 있도록 설계되어야 합니다. 특정 소스를 제거하고 청크를 재발행하는 절차는 다음과 같습니다.

```bash
# 1. 침해 소스를 파이프라인 필터에서 제외
# tools/data-pipeline/src/config/sources.ts 에서 해당 소스 비활성화

# 2. 해당 소스 데이터만 제외하고 재처리
npm run pipeline -- --exclude-source <source-name>

# 3. 새 버전의 청크 아카이브 생성
npm run pack -- --version content-v2

# 4. 기존 배포 URL(content-v1)을 새 버전(content-v2)으로 교체
# GitHub Releases에서 이전 릴리스 제거 및 새 릴리스 퍼블리시

# 5. 앱의 매니페스트 URL 업데이트하여 새 버전 청크 참조
```

> **검토 필요**: 현재 파이프라인 코드가 소스별 메타데이터(source_id 필드 등)를 JSONL 레코드에 유지하는지 확인하십시오. 소스 추적이 불가능하면 침해 소스 데이터를 선별 제거하기 어렵습니다.

### 6.3 반박 신고 (Counter-Notice) 절차

신고가 유효하지 않다고 판단되는 경우(예: CC 라이선스 조건을 실제로 준수하고 있음에도 신고된 경우), 법률 자문을 거쳐 플랫폼(Google Play)에 반박 신고(DMCA counter-notice)를 제출할 수 있습니다.

---

## 참고 문서

- [[01-license-audit]] — 의존성 라이선스 전수 조사
- [[02-license-compatibility]] — 라이선스 호환성 분류
- [[03-distribution-structure]] — 저장소 및 배포물 구성
- [[05-proprietary-license]] — Proprietary License 명시
