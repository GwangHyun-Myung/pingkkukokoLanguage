---
date: 2026-05-04
type: index
scope: data
related: [[01-license-audit]], [[02-license-compatibility]], [[03-distribution-structure]], [[04-code-rights-protection]], [[05-proprietary-license]]
---

# datas/ — 콘텐츠 데이터 및 라이선스 문서 인덱스

## 1. 개요

`datas/` 디렉토리는 pingkkukoko 언어 학습 앱이 사용하는 콘텐츠 데이터와, 그 데이터의 출처·라이선스·배포 구조에 관한 법적 참고 문서를 담고 있습니다. 이 디렉토리는 공개 데이터 소스(Creative Commons / 퍼블릭 도메인 (public domain))에서 파생된 콘텐츠와 그에 대한 라이선스 문서를 담고 있습니다. 앱 측 코드는 `../apps/`에 별도 분리되어 있습니다.

콘텐츠 데이터(`content-v1/`)는 앱에 번들링되지 않습니다. 최초 실행 시 GitHub에서 다운로드되어 로컬 SQLite DB에 시드됩니다. 라이선스 문서 5편(`01~05`)은 데이터 측 권리 관계를 단계적으로 분석한 내부 참고 자료입니다.

## 2. 디렉토리 구조

```
datas/
├── README.md                      ← 이 파일
├── 01-license-audit.md
├── 02-license-compatibility.md
├── 03-distribution-structure.md
├── 04-code-rights-protection.md
├── 05-proprietary-license.md
└── content-v1/
    ├── manifest.json
    ├── words/
    │   ├── en-tier1-001.jsonl.gz
    │   ├── en-tier2-001.jsonl.gz
    │   ├── en-tier3-001.jsonl.gz
    │   ├── en-tier3-002.jsonl.gz
    │   ├── en-tier3-003.jsonl.gz
    │   ├── en-tier3-004.jsonl.gz
    │   ├── es-tier1-001.jsonl.gz
    │   ├── es-tier2-001.jsonl.gz
    │   ├── es-tier3-001.jsonl.gz
    │   ├── ja-tier1-001.jsonl.gz
    │   ├── ja-tier1-002.jsonl.gz
    │   ├── ja-tier2-001.jsonl.gz
    │   ├── ja-tier3-001.jsonl.gz
    │   ├── ko-tier1-001.jsonl.gz
    │   ├── ko-tier2-001.jsonl.gz
    │   ├── ko-tier3-001.jsonl.gz
    │   ├── zh-tier1-001.jsonl.gz
    │   ├── zh-tier2-001.jsonl.gz
    │   └── zh-tier3-001.jsonl.gz
    └── sentences/
        ├── en-tier1-001.jsonl.gz
        ├── en-tier1-002.jsonl.gz
        ├── en-tier1-003.jsonl.gz
        ├── en-tier2-001.jsonl.gz
        ├── en-tier2-002.jsonl.gz
        ├── en-tier3-001.jsonl.gz
        ├── es-tier1-001.jsonl.gz
        ├── es-tier2-001.jsonl.gz
        ├── es-tier3-001.jsonl.gz
        ├── ja-tier1-001.jsonl.gz
        ├── ja-tier1-002.jsonl.gz
        ├── ja-tier1-003.jsonl.gz
        ├── ja-tier2-001.jsonl.gz
        ├── ja-tier3-001.jsonl.gz
        ├── ko-tier1-001.jsonl.gz
        ├── ko-tier2-001.jsonl.gz
        ├── ko-tier3-001.jsonl.gz
        ├── ko-tier3-002.jsonl.gz
        ├── ko-tier3-003.jsonl.gz
        ├── zh-tier1-001.jsonl.gz
        ├── zh-tier2-001.jsonl.gz
        └── zh-tier3-001.jsonl.gz
```

청크 파일명 패턴: `<언어코드>-<티어>-<순번>.jsonl.gz`

## 3. 라이선스 문서 색인

| 단계 | 문서 | 내용 |
|------|------|------|
| 1단계 | [[01-license-audit]] | 사용된 모든 외부 데이터 소스(WordNet, Wiktionary, Tatoeba 등) 라이선스 전수 조사 |
| 2단계 | [[02-license-compatibility]] | CC-BY-SA × CC-BY × BSD × 퍼블릭 도메인 호환성 분석 |
| 3단계 | [[03-distribution-structure]] | 청크 아카이브 구성 및 호스팅 위치 |
| 4단계 | [[04-code-rights-protection]] | 데이터 측 권리 보호 및 DMCA 대응 절차 |
| 5단계 | [[05-proprietary-license]] | 큐레이션·구조 결정에 대한 Proprietary License (CC 원천 데이터 자체에는 적용되지 않음) |

## 4. 콘텐츠 통계

| 항목 | 값 |
|------|-----|
| 총 청크 수 | 41 (단어 19 + 문장 22) |
| 총 압축 크기 | ~141 MB |
| 총 비압축 크기 | ~728 MB |
| 지원 언어 | 영어 (en), 중국어 (zh), 스페인어 (es), 일본어 (ja), 한국어 (ko) |
| 단어 레코드 | ~1,101,309 (5언어 합계) |
| 문장 레코드 | ~1,053,023 (5언어 합계) |
| 난이도 티어 | tier1 (CEFR A1-A2), tier2 (B1), tier3 (B2-C1+) |
| 매니페스트 버전 | 1.0.0 |

## 5. 호스팅 위치

콘텐츠 청크는 별도 공개 저장소에 호스팅됩니다.

- **저장소**: `https://github.com/GwangHyun-Myung/pingkkukokoLanguage`
- **기본 브랜치**: `mbase`
- **매니페스트 URL**:
  ```
  https://raw.githubusercontent.com/GwangHyun-Myung/pingkkukokoLanguage/mbase/content-v1/manifest.json
  ```
- **청크 URL 패턴**:
  ```
  https://raw.githubusercontent.com/GwangHyun-Myung/pingkkukokoLanguage/mbase/content-v1/<chunkPath>
  ```
- **jsDelivr CDN 대안** (캐시 안정성이 필요한 경우):
  ```
  https://cdn.jsdelivr.net/gh/GwangHyun-Myung/pingkkukokoLanguage@mbase/content-v1/<path>
  ```

앱은 최초 실행 시 매니페스트를 먼저 내려받아 청크 목록과 체크섬을 확인한 뒤, 각 청크를 순차 다운로드하여 SQLite에 시드합니다.

## 6. 외부 데이터 소스

### 사전 데이터 (Lexical sources)

| 소스 | 관리 주체 | 라이선스 |
|------|----------|---------|
| [WordNet 3.1](https://wordnet.princeton.edu/) | Princeton University | [WordNet License](https://wordnet.princeton.edu/license-and-commercial-use) (퍼블릭 도메인에 준하는 BSD-style) |
| [Wiktionary](https://www.wiktionary.org/) (en/es/ko) | Wikimedia Contributors | [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) + GFDL |
| [CC-CEDICT](https://cc-cedict.org/) | MDBG | [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |
| [JMdict / EDICT2](https://www.edrdg.org/jmdict/j_jmdict.html) | EDRDG | [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |

### 문장 데이터 (Sentence corpora)

| 소스 | 관리 주체 | 라이선스 |
|------|----------|---------|
| [Tatoeba](https://tatoeba.org/) | Tatoeba Contributors | [CC-BY 2.0 FR](https://creativecommons.org/licenses/by/2.0/fr/) |
| [WikiMatrix](https://opus.nlpl.eu/WikiMatrix.php) | Schwenk et al. (OPUS) | [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |
| [Project Gutenberg](https://www.gutenberg.org/) | 다수 기여자 | 퍼블릭 도메인 (작품별 확인 필요) |

소스별 상세 라이선스 조건은 [[01-license-audit]] 참조.

## 7. 라이선스 요약

| 대상 | 라이선스 |
|------|---------|
| 콘텐츠 청크 (`content-v1/`) | **CC-BY-SA 4.0** — 대부분의 원천이 공유 의무 (share-alike) 부과 |
| 라이선스 문서 (`01~05`) | 프로젝트 내부 참고 자료 |
| 큐레이션·청킹 구조 결정 (`manifest.json` 스키마 등) | Proprietary 보유 ([[05-proprietary-license]] 참조) |

CC-BY-SA 4.0의 공유 의무는 **원천 데이터에서 파생된 콘텐츠**에 적용됩니다. 앱 코드(`../apps/`)는 별도 저작물로서 이 의무의 적용을 받지 않습니다. 호환성 분석의 전체 내용은 [[02-license-compatibility]] 참조.

## 8. 문의

라이선스 또는 콘텐츠 관련 문의: `prozect@hanmail.net`
