---
date: 2026-05-03
type: legal-policy
step: 1
related: [[02-license-compatibility]], [[03-distribution-structure]], [[04-code-rights-protection]], [[05-proprietary-license]]
---

# 01 — 의존성 라이선스 전수 조사 (Dependency License Audit)

> **면책 고지**: 이 문서는 프로젝트 내부 참고용 자료이며 법적 조언(legal advice)이 아닙니다. 라이선스 준수 여부에 관한 최종 판단은 반드시 자격을 갖춘 변호사(attorney)에게 검토를 의뢰하십시오.

---

## 1. 개요

이 문서는 pingkkukoko 앱에 사용된 외부 데이터 소스(data source) 및 빌드 도구(build-time tooling) 전체를 대상으로 라이선스 현황을 조사한 결과입니다. 조사 대상은 다음 두 가지 범주로 나뉩니다.

1. **데이터 소스 (Data Sources)** — 앱 번들 또는 다운로드 청크로 배포되는 어휘·문장 데이터의 원천.
2. **빌드 도구 (Build-time Tooling)** — 데이터 파이프라인(`tools/data-pipeline/`) 실행에 사용되는 Node.js 패키지. 앱 번들에 포함되지 않으므로 최종 배포물의 라이선스 요건에는 직접 영향을 주지 않지만, 완전성을 위해 기록합니다.

### 1.1 파생 저작물(Derivative Work) 지위

파이프라인이 수집·처리한 데이터는 원천 소스를 **그대로 복사한 것이 아닙니다**. 파이프라인은 다음 변환을 수행합니다.

- XML/위키 마크업 파싱 후 구조화된 JSONL 형식으로 변환
- 언어별 필터링, 품질 점수(quality score) 기반 정제
- 학습 앱 스키마에 맞게 필드 재구성 (enrichment)
- 중복 제거 및 교차 소스(cross-source) 병합

저작권법상 이 같은 선택·배열·변환은 **편집저작물(compilation) 또는 2차적저작물(derivative work)** 에 해당할 수 있습니다. CC-BY-SA 4.0 라이선스의 경우, 2차적저작물을 배포할 때 동일한 라이선스(share-alike) 조건을 적용할 의무가 발생합니다. 각 소스의 파생 지위가 라이선스 의무에 미치는 영향은 `[[02-license-compatibility]]`에서 상세히 분석합니다.

---

## 2. 어휘·사전 소스 (Lexical / Dictionary Sources)

출력 위치: `tools/data-pipeline/out/words/<lang>.jsonl`

| # | 소스 이름 | 대상 언어 | 버전 / 덤프 날짜 | 라이선스 | 원문 URL | 저작자 표시 (Attribution) 필요 | Share-alike 요건 | 상업적 이용 허용 | 재배포 허용 |
|---|-----------|----------|-----------------|----------|----------|-------------------------------|-----------------|----------------|------------|
| 1 | **WordNet 3.1** (Princeton University) | en | 3.1 | WordNet License (BSD-style) | https://wordnetcode.princeton.edu/wn3.1.dict.tar.gz | 필요 — Princeton 저작권 문구 유지 | **없음** | 허용 | 허용 (조건부) |
| 2 | **English Wiktionary** 덤프 | en, ko | 최신 덤프 | CC-BY-SA 4.0 + GFDL | https://dumps.wikimedia.org/enwiktionary/ | 필요 — Wiktionary 기여자 표시 | **있음** (CC-BY-SA) | 허용 | 허용 (동일 조건) |
| 3 | **Spanish Wiktionary** 덤프 | es | 최신 덤프 | CC-BY-SA 4.0 + GFDL | https://dumps.wikimedia.org/eswiktionary/ | 필요 | **있음** (CC-BY-SA) | 허용 | 허용 (동일 조건) |
| 4 | **Korean Wiktionary** 덤프 | ko | 최신 덤프 | CC-BY-SA 4.0 + GFDL | https://dumps.wikimedia.org/kowiktionary/ | 필요 | **있음** (CC-BY-SA) | 허용 | 허용 (동일 조건) |
| 5 | **CC-CEDICT** (MDBG) | zh | 최신 릴리스 | CC-BY-SA 4.0 | https://www.mdbg.net/chinese/dictionary?page=cc-cedict | 필요 — MDBG 및 기여자 표시 | **있음** (CC-BY-SA) | 허용 | 허용 (동일 조건) |
| 6 | **JMdict / EDICT2** (EDRDG) | ja | JMdict 최신 | CC-BY-SA 4.0 (EDRDG License) | https://www.edrdg.org/jmdict/edict_doc.html | 필요 — EDRDG 저작권 문구 유지 | **있음** (CC-BY-SA) | 허용 (EDRDG 조건 확인 권장) | 허용 (동일 조건) |

### 2.1 파생 지위별 라이선스 영향

| 소스 | 파생 지위 | 라이선스 의무 |
|------|----------|--------------|
| WordNet 3.1 | 파생저작물 (필드 재구성) | Princeton 저작권 문구 유지; share-alike 없음 → 가장 자유로운 소스 |
| Wiktionary (en/es/ko) | 파생저작물 (마크업→JSONL 변환) | CC-BY-SA 4.0 조건 충족 필요; 결과물에도 CC-BY-SA 4.0 적용 |
| CC-CEDICT | 파생저작물 (정제·필터링) | CC-BY-SA 4.0 조건 충족 필요 |
| JMdict | 파생저작물 (정제·필터링) | CC-BY-SA 4.0 + EDRDG 별도 조항 확인 필요 |

> **검토 필요**: JMdict의 EDRDG 라이선스는 CC-BY-SA 4.0 채택 이전의 별도 조항을 포함하고 있습니다. 상업 배포 전 EDRDG의 최신 라이선스 문서(https://www.edrdg.org/edrdg/licence.html)를 반드시 재확인하십시오.

---

## 3. 문장 코퍼스 소스 (Sentence Corpus Sources)

출력 위치: `tools/data-pipeline/out/sentences/<lang>.jsonl`

| # | 소스 이름 | 대상 언어 | 버전 / 덤프 날짜 | 라이선스 | 원문 URL | 저작자 표시 필요 | Share-alike 요건 | 상업적 이용 허용 | 재배포 허용 |
|---|-----------|----------|-----------------|----------|----------|----------------|-----------------|----------------|------------|
| 1 | **Tatoeba** | en/zh/es/ja/ko (교차 쌍) | 최신 내보내기 | CC-BY 2.0 FR | https://tatoeba.org | 필요 — Tatoeba 및 개별 기여자 표시 | **없음** | 허용 | 허용 |
| 2 | **WikiMatrix** (OPUS / Schwenk et al. 2019) | 전체 (ko-pair) | OPUS 버전 | CC-BY-SA 4.0 (Wikipedia 기반 채굴) | https://opus.nlpl.eu/WikiMatrix.php | 필요 | **있음** (CC-BY-SA) | 허용 | 허용 (동일 조건) |
| 3 | **Project Gutenberg** | en (고전 50편) | 개별 작품별 | Public Domain (1928년 이전 미국 저작권법 기준) | https://www.gutenberg.org | 불필요 (저작권 소멸) — 단, Project Gutenberg 트레이드마크(trademark) 표시 별도 확인 | **없음** | 허용 | 허용 |

### 3.1 파생 지위별 라이선스 영향

| 소스 | 파생 지위 | 라이선스 의무 |
|------|----------|--------------|
| Tatoeba | 선별(selection) — 편집저작물 | CC-BY 2.0 FR; share-alike 없으므로 재배포 시 CC-BY 표시만 충족하면 됨 |
| WikiMatrix | 파생저작물 (Wikipedia 텍스트 채굴) | CC-BY-SA 4.0; 결과물에 동일 조건 적용 |
| Project Gutenberg | 공중 영역(public domain) 원문 발췌 | 저작권 제약 없음; Project Gutenberg 트레이드마크는 별도 고려 필요 |

> **참고**: Tatoeba의 CC-BY 2.0 FR(프랑스 준거법)은 CC-BY 4.0과 호환성이 높지만 완전히 동일하지는 않습니다. 배포 시 원본 라이선스 표기를 그대로 유지하는 것이 권장됩니다.

> **Project Gutenberg 트레이드마크 주의**: 텍스트 자체는 퍼블릭 도메인(public domain)이나, "Project Gutenberg" 명칭과 로고는 Project Gutenberg Literary Archive Foundation의 트레이드마크입니다. 소스 원문 출처를 표시할 때 이 이름을 사용하는 것은 적법하지만, 이 이름을 브랜딩(branding) 목적으로 전용하는 것은 허용되지 않습니다.

---

## 4. 빌드 도구 (Build-time Tooling)

이 패키지들은 `tools/data-pipeline/` 파이프라인 실행에만 사용되며, **앱 번들에 포함되지 않습니다**. 따라서 이 패키지의 라이선스가 최종 배포물의 데이터 라이선스에 영향을 주지 않습니다. 아래 표는 파이프라인 운영 환경(build environment) 감사 목적으로 기록합니다.

| 패키지 | 버전 (package.json 참조) | 라이선스 | 배포물 포함 여부 |
|--------|--------------------------|----------|----------------|
| `tsx` | — | MIT | **아니오** |
| `typescript` | — | Apache-2.0 | **아니오** |
| `yargs` | — | MIT | **아니오** |
| `sax` | — | ISC | **아니오** |
| `pino` | — | MIT | **아니오** |
| `pino-pretty` | — | MIT | **아니오** |
| `unbzip2-stream` | — | MIT | **아니오** |
| `unzipper` | — | MIT | **아니오** |
| `@types/node` | — | MIT | **아니오** |
| `@types/yargs` | — | MIT | **아니오** |
| `@types/sax` | — | MIT | **아니오** |
| `@types/unzipper` | — | MIT | **아니오** |

> 빌드 도구 패키지는 모두 MIT, ISC, 또는 Apache-2.0 라이선스로, 상업적 사용 및 재배포에 있어 가장 자유로운 조건을 제공합니다. 이들을 소스로 제공하거나 배포할 경우에는 각 패키지의 원본 LICENSE 파일을 동봉해야 합니다.

---

## 5. 원시 데이터 위치 (Raw Data Location)

파이프라인이 원천 소스로부터 다운로드한 원본 덤프 파일들은 다음 경로에 캐시됩니다.

```
tools/data-pipeline/raw/
```

이 디렉토리는 `.gitignore`에 등록되어 있어 버전 관리에 포함되지 않습니다. 이유는 다음과 같습니다.

- 파일 크기가 수백 MB에 달해 git 저장소에 적합하지 않음
- 각 소스의 라이선스에 따라 소스 덤프를 직접 재배포하는 것 자체가 허용되지 않을 수 있음
- 재현 가능성(reproducibility)은 소스 URL과 파이프라인 코드로 보장됨

**추적 가능성(Traceability)**: 각 원본 덤프의 다운로드 URL 및 예상 SHA-256 체크섬은 파이프라인 설정 파일 또는 별도의 `tools/data-pipeline/SOURCES.lock` 파일로 관리하는 것을 권장합니다. 이 잠금 파일(lock file)은 어떤 버전의 원본 데이터가 어느 버전의 앱 데이터를 생성했는지 감사(audit) 시 추적할 수 있는 근거가 됩니다.

---

## 참고 문서

- [[02-license-compatibility]] — 라이선스 호환성 분류 및 Share-alike 전염 분석
- [[03-distribution-structure]] — 저장소 및 배포물 구성
- [[04-code-rights-protection]] — 자체 코드의 권리 보호
- [[05-proprietary-license]] — Proprietary License 명시
