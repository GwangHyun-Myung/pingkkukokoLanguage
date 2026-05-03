---
date: 2026-05-03
type: legal-policy
step: 2
related: [[01-license-audit]], [[03-distribution-structure]], [[04-code-rights-protection]], [[05-proprietary-license]]
---

# 02 — 라이선스 호환성 분류 (License Compatibility Analysis)

> **면책 고지**: 이 문서는 프로젝트 내부 참고용 자료이며 법적 조언(legal advice)이 아닙니다. 라이선스 호환성에 관한 최종 판단은 반드시 자격을 갖춘 변호사(attorney)에게 검토를 의뢰하십시오.

---

## 1. 개요

pingkkukoko의 번들 데이터는 여러 오픈 라이선스(open license)가 혼재합니다. 이 문서는 각 라이선스가 단일 배포 단위(distribution unit)로 결합될 때 어떤 조건이 적용되는지를 분석하고, 프로젝트가 채택해야 할 라이선스 계층 구조(layered licensing structure)를 도출합니다.

---

## 2. 호환성 매트릭스 (Compatibility Matrix)

아래 표는 두 라이선스를 결합하여 단일 저작물로 배포할 때의 허용 여부를 나타냅니다.

| | **Proprietary (All Rights Reserved)** | **CC-BY 4.0 / 2.0 FR** | **CC-BY-SA 4.0** | **WordNet (BSD-style)** | **Public Domain** |
|---|---|---|---|---|---|
| **Proprietary** | ✅ 가능 | ⚠️ 집합(aggregation)으로만 가능 | ⚠️ 집합으로만 가능 | ✅ 가능 (BSD 조건 충족 시) | ✅ 가능 |
| **CC-BY 4.0 / 2.0 FR** | ⚠️ 집합으로만 가능 | ✅ 가능 | ✅ 가능 (SA 조건 적용됨) | ✅ 가능 | ✅ 가능 |
| **CC-BY-SA 4.0** | ⚠️ 집합으로만 가능 | ✅ 가능 (SA 조건 적용됨) | ✅ 가능 | ✅ 가능 (SA 조건 적용됨) | ✅ 가능 (SA 조건 적용됨) |
| **WordNet (BSD-style)** | ✅ 가능 | ✅ 가능 | ✅ 가능 (SA 조건 적용됨) | ✅ 가능 | ✅ 가능 |
| **Public Domain** | ✅ 가능 | ✅ 가능 | ✅ 가능 (SA 조건 적용됨) | ✅ 가능 | ✅ 가능 |

**범례**
- ✅ 가능: 별도 제약 없이 결합 가능
- ⚠️ 집합으로만 가능: 파일 또는 배포 단위를 명확히 분리하여 "집합저작물(mere aggregation)"로 처리할 때에만 허용. 하나의 통합 파생저작물로 결합하면 라이선스 충돌 발생.

---

## 3. Share-alike 전염 분석 (Share-alike Propagation Analysis)

Share-alike(동일조건변경허락)은 CC-BY-SA 및 일부 오픈 라이선스에서 2차적저작물(derivative work)에 원 라이선스를 동일하게 적용하도록 요구하는 조건입니다. "전염(viral)"이라고도 불리는 이 특성은 결합 방식에 따라 배포 전략에 결정적인 영향을 미칩니다.

### 3.1 Share-alike가 전파되는 경우

다음 조건이 동시에 충족될 때 CC-BY-SA 4.0의 share-alike 조건이 전체 결합물에 전파됩니다.

1. CC-BY-SA 4.0 소스 데이터를 변환·편집하여 **2차적저작물**을 생성한 경우
2. 해당 2차적저작물을 **단일 배포 단위**로 패키징하여 배포한 경우

pingkkukoko의 경우, Wiktionary/CC-CEDICT/JMdict/WikiMatrix 데이터를 JSONL로 변환하고 앱 스키마에 맞게 가공한 결과물은 2차적저작물에 해당합니다. 따라서 이 데이터를 배포할 때는 CC-BY-SA 4.0 조건이 적용됩니다.

### 3.2 Share-alike가 전파되지 않는 경우

다음의 상황에서는 share-alike가 **앱 코드 전체에 전파되지 않습니다**.

| 상황 | 이유 |
|------|------|
| 앱 코드와 데이터가 서로 다른 파일·아카이브로 완전히 분리된 경우 | 집합저작물(mere aggregation)로 처리되어 각 구성 요소의 라이선스가 독립적으로 유지됨 |
| 앱이 데이터를 런타임에 외부에서 다운로드하는 경우 | APK 배포 시점에 CC 데이터가 번들에 포함되지 않으므로 share-alike 전파 없음 |
| WordNet(BSD-style) 데이터만 별도로 포함되는 경우 | WordNet 라이선스는 share-alike 없음 |

---

## 4. 집합저작물과 2차적저작물의 법적 구별 (Aggregation vs. Derivation)

이 구별은 pingkkukoko의 배포 전략에서 가장 중요한 법적 레버(legal lever)입니다.

### 4.1 정의

- **2차적저작물(Derivative Work)**: 원저작물을 번역·편곡·변형·각색하거나 다른 방식으로 변환하여 새롭게 창작한 저작물. 원저작물의 표현이 새 저작물에 녹아 들어가 분리가 불가능한 상태.
- **집합저작물(Mere Aggregation)**: 서로 다른 저작물을 단순히 한 매체(CD, 아카이브, 앱스토어 페이지 등)에 모아 놓은 것. 각 저작물이 독립성을 유지하며 상호 통합되지 않음.

CC 라이선스는 이 구별을 명시적으로 인정합니다: "단순한 집합(mere aggregation)은 라이선스 조건을 다른 저작물로 확장시키지 않는다."

### 4.2 pingkkukoko에 적용

| 배포 시나리오 | 분류 | 결론 |
|-------------|------|------|
| APK 내 앱 코드 + 별도 다운로드 데이터 청크 | **집합** | APK 코드에 share-alike 전파 없음 ✅ |
| APK 내에 CC-BY-SA 데이터가 직접 번들링된 경우 | **파생(또는 집합 경계 불명확)** | share-alike 적용 가능성 — 권장하지 않음 ⚠️ |
| `apps/src/data/<lang>/unit1.json` (10개 레코드) APK 내 포함 | **파생** (CC-BY-SA 원천에서 변환) | CC-BY-SA 4.0 의무 발생; 출처 표시 필수 ⚠️ |
| `datas/content-v1/*.jsonl.gz` GitHub Releases 별도 배포 | **집합 또는 파생** (배포 단위 분리) | CC-BY-SA 4.0 의무 발생; APK 코드와는 독립 ✅ |

> **핵심 결론**: pingkkukoko가 CC 데이터를 런타임에 외부 URL에서 다운로드하는 아키텍처를 유지하는 한, APK 자체는 독점 소프트웨어(proprietary software)로서 배포 가능합니다. 단, APK에 번들된 소량 데이터(`unit1.json` 등)는 CC-BY-SA 조건을 충족해야 합니다.

---

## 5. 권장 라이선스 계층 분류 (Recommended License Layers)

### 레이어 1: Proprietary Layer (독점 레이어)

**포함 대상**
- `apps/src/` 내 모든 TypeScript/TSX 소스 코드
- UI 자산(이미지, 아이콘, 애니메이션)
- 앱 셸(app shell), 내비게이션 구조, 게이미피케이션 로직
- 빌드 설정, CI/CD 구성
- `tools/data-pipeline/src/` 내 파이프라인 소스 코드

**적용 라이선스**: All Rights Reserved (전체 권리 보유)

**조건**: 이 레이어는 CC 라이선스 데이터와 파일 수준에서 명확히 분리되어야 합니다.

### 레이어 2: Aggregated CC-BY-SA 4.0 Layer (CC 데이터 레이어)

**포함 대상**
- `apps/src/data/<lang>/unit*.json` (APK 번들 내 10개 레코드 코어)
- `datas/content-v1/*.jsonl.gz` (GitHub Releases 등에서 배포되는 청크)

**적용 라이선스**: Creative Commons Attribution-ShareAlike 4.0 International (CC-BY-SA 4.0)

**조건**:
- 앱 내 저작자 표시(attribution) 화면 필수
- 데이터 아카이브에 `LICENSE.txt` + `ATTRIBUTIONS.txt` 동봉 필수
- 재배포 시 동일 CC-BY-SA 4.0 조건 적용

**참고**: Tatoeba 데이터는 CC-BY 2.0 FR이므로 share-alike 없이 포함 가능합니다. 그러나 CC-BY-SA 소스와 혼합된 데이터 파일 단위로는 CC-BY-SA 4.0을 전체 적용하는 것이 실무상 가장 안전합니다.

### 레이어 3: Public Domain Layer (퍼블릭 도메인 레이어)

**포함 대상**
- Project Gutenberg 원전(en, pre-1928) 발췌 문장

**적용 라이선스**: Public Domain (저작권 소멸)

**조건**: 저작권 제약 없음. 단, Project Gutenberg 트레이드마크 사용 정책 별도 준수 필요. 이 데이터는 CC-BY-SA 데이터와 혼합되어 동일 파일에 포함될 경우 해당 파일 전체에 CC-BY-SA가 적용될 수 있으므로, 별도 파일로 분리하거나 혼합을 명시적으로 허용하는 정책을 수립하는 것을 권장합니다.

---

## 6. 결론: 각 배포 산출물에 적용되는 라이선스

| 배포 산출물 | 적용 라이선스 | 핵심 의무 |
|------------|--------------|----------|
| **Play Store APK (코드 + 10개 레코드)** | 앱 코드: Proprietary / 번들 데이터: CC-BY-SA 4.0 | 앱 내 저작자 표시 화면 필수; NOTICES 파일 포함 권장 |
| **`apps/src/data/<lang>/unit*.json`** | CC-BY-SA 4.0 | 출처 표시, 동일 라이선스 적용 |
| **`datas/content-v1/*.jsonl.gz` (청크)** | CC-BY-SA 4.0 | 아카이브에 LICENSE.txt + ATTRIBUTIONS.txt 포함 |
| **빌드 도구 (`tools/data-pipeline/`)** | MIT / ISC / Apache-2.0 (각 패키지별) | 앱 배포에 영향 없음; 파이프라인 배포 시 각 패키지 라이선스 준수 |
| **Project Gutenberg 발췌 데이터** | Public Domain | 저작권 제약 없음; 트레이드마크 정책 별도 확인 |

---

## 참고 문서

- [[01-license-audit]] — 의존성 라이선스 전수 조사
- [[03-distribution-structure]] — 저장소 및 배포물 구성
- [[04-code-rights-protection]] — 자체 코드의 권리 보호
- [[05-proprietary-license]] — Proprietary License 명시
