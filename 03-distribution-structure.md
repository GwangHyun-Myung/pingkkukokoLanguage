---
date: 2026-05-03
type: legal-policy
step: 3
related: [[01-license-audit]], [[02-license-compatibility]], [[04-code-rights-protection]], [[05-proprietary-license]]
---

# 03 — 저장소 및 배포물 구성 (Distribution Structure)

> **면책 고지**: 이 문서는 프로젝트 내부 참고용 자료이며 법적 조언(legal advice)이 아닙니다. 배포 전 자격을 갖춘 변호사(attorney)의 검토를 권장합니다.

---

## 1. 개요

이 문서는 pingkkukoko 프로젝트가 라이선스 준수(license compliance)를 실현하기 위한 파일 구조와 배포 산출물(distribution artifact)의 구성 방식을 정의합니다. `[[02-license-compatibility]]`에서 도출한 3계층 라이선스 분류를 실제 디렉토리 구조와 배포 패키지에 어떻게 반영할지를 명시합니다.

---

## 2. 소스 저장소 구조 (Source Repository Structure)

### 2.1 전체 구조

```
pingkkukoko/                         ← 저장소 루트
├── apps/                            ← Expo/React Native 앱 (독점 레이어)
│   ├── LICENSE                      ← [생성 예정] Proprietary License
│   ├── src/
│   │   ├── data/
│   │   │   ├── en/unit1.json        ← CC-BY-SA 4.0 (번들 코어, 10개 레코드)
│   │   │   ├── zh/unit1.json
│   │   │   ├── ja/unit1.json
│   │   │   ├── ko/unit1.json
│   │   │   └── es/unit1.json
│   │   ├── components/              ← 독점 코드
│   │   ├── services/                ← 독점 코드
│   │   ├── store/                   ← 독점 코드
│   │   └── ...
│   └── package.json
│
├── tools/                           ← 빌드 도구 (독점 레이어)
│   ├── LICENSE                      ← [생성 예정] Proprietary License
│   └── data-pipeline/
│       ├── raw/                     ← .gitignore 처리됨 (원본 덤프 캐시)
│       ├── out/                     ← 파이프라인 출력 (중간 산출물)
│       └── src/                     ← 파이프라인 소스 코드
│
├── datas/                           ← CC 파생 데이터 레이어
│   ├── LICENSE                      ← [생성 예정] CC-BY-SA 4.0 전문
│   ├── ATTRIBUTIONS.md              ← [생성 예정] 모든 업스트림 소스 표시
│   ├── content-v1/                  ← 청크 아카이브 (다운로드 대상)
│   │   ├── en-words-001.jsonl.gz
│   │   ├── zh-words-001.jsonl.gz
│   │   └── ...
│   ├── 01-license-audit.md          ← 이 문서들
│   ├── 02-license-compatibility.md
│   ├── 03-distribution-structure.md
│   ├── 04-code-rights-protection.md
│   └── 05-proprietary-license.md
│
├── docs/                            ← 프로젝트 문서
├── build/                           ← EAS 빌드 설정
└── .gitignore
```

### 2.2 레이어별 LICENSE 파일 배치

| 디렉토리 | LICENSE 파일 내용 | 상태 |
|---------|-----------------|------|
| `apps/LICENSE` | Proprietary License (All Rights Reserved) — `[[05-proprietary-license]]` 참조 | 생성 예정 |
| `tools/LICENSE` | Proprietary License (All Rights Reserved) | 생성 예정 |
| `datas/LICENSE` | CC-BY-SA 4.0 전문 (Creative Commons Corporation 공식 텍스트 링크 포함) | 생성 예정 |
| `datas/ATTRIBUTIONS.md` | 모든 업스트림 소스 저작자 표시 목록 | 생성 예정 |

> **참고**: 위 LICENSE 파일들은 이 문서 세트가 확정된 후 별도로 생성합니다. 현 시점에서는 이 문서(`03-distribution-structure.md`)가 각 LICENSE 파일의 내용 기준(reference specification)으로 기능합니다.

---

## 3. 배포 산출물 구성 (Distribution Artifacts)

### 3.1 Play Store APK

**포함 내용**
- 앱 코드 전체 (독점 레이어)
- 각 언어별 10개 레코드 코어 데이터 (`apps/src/data/<lang>/unit1.json`)

**라이선스 준수 요건**

| 요건 | 방법 | 우선순위 |
|------|------|---------|
| 앱 내 저작자 표시 화면 | 설정(Settings) 또는 정보(About) 화면에 크레딧 섹션 구현 | **필수** |
| NOTICES 파일 | APK 내 `assets/NOTICES.txt` 또는 `META-INF/NOTICES` 포함 | 권장 |
| CC-BY-SA 4.0 라이선스 본문 링크 | 앱 내 크레딧 화면에서 https://creativecommons.org/licenses/by-sa/4.0/ 링크 | **필수** |

### 3.2 사이드로드 배포 (Sideload Distribution)

APK를 Play Store 외부에서 직접 배포하는 경우:

**포함 내용**
- APK 파일
- 데이터 청크 ZIP 아카이브 (또는 링크)

**라이선스 준수 요건**
- APK와 함께 `LICENSE.txt`, `ATTRIBUTIONS.txt` 동봉 또는 동반 URL 안내 필수
- 데이터 청크 아카이브 내에도 동일 파일 포함 필수

### 3.3 URL 호스팅 청크 (GitHub Releases / CDN)

`datas/content-v1/*.jsonl.gz` 파일을 GitHub Releases 또는 외부 CDN에 호스팅하는 경우:

**옵션 A — 아카이브 내 포함 (권장)**
각 `.jsonl.gz` 파일을 압축 해제하면 최상위에 다음 파일이 존재하도록 구성:
```
en-words-001/
├── LICENSE.txt         ← CC-BY-SA 4.0 전문
├── ATTRIBUTIONS.txt    ← 원천 소스 목록
└── data.jsonl          ← 실제 데이터
```

**옵션 B — 매니페스트 페치 (Manifest Fetch) 방식**
앱이 첫 실행 시 청크 목록과 함께 라이선스 메타데이터 URL을 서버에서 수신. 라이선스 본문은 별도 URL로 제공하고, 앱 크레딧 화면에서 이를 참조.

> **권장**: 옵션 A가 아카이브 자체에 라이선스를 포함시키므로, 파일이 재배포되더라도 라이선스 정보가 분리되지 않아 더 안전합니다.

---

## 4. 앱 내 저작자 표시 화면 (In-App Attribution Screen)

### 4.1 화면 위치

앱 내비게이션 트리에서 `(tabs)/settings` 또는 별도의 `About` 화면에 "오픈 소스 라이선스 및 데이터 출처" 섹션을 구현합니다.

### 4.2 표시해야 할 크레딧 텍스트 (샘플 — 실제 앱에 반영 필요)

---

**앱 내 크레딧 화면 샘플 텍스트 (한국어)**

---

**데이터 출처 및 라이선스 안내**

이 앱은 다음의 공개 데이터 소스로부터 파생된 언어 학습 콘텐츠를 포함합니다.

**사전 데이터 (단어)**

- **WordNet 3.1** — Princeton University 제공. WordNet License 적용.
  https://wordnet.princeton.edu/license-and-commercial-use

- **Wiktionary** (영어, 스페인어, 한국어판) — Wikimedia 기여자 제공.
  Creative Commons Attribution-ShareAlike 4.0 International (CC-BY-SA 4.0) 및 GFDL 적용.
  https://creativecommons.org/licenses/by-sa/4.0/

- **CC-CEDICT** — MDBG 및 기여자 제공.
  Creative Commons Attribution-ShareAlike 4.0 International (CC-BY-SA 4.0) 적용.
  https://creativecommons.org/licenses/by-sa/4.0/

- **JMdict / EDICT2** — Electronic Dictionary Research and Development Group (EDRDG) 제공.
  Creative Commons Attribution-ShareAlike 4.0 International (CC-BY-SA 4.0) 적용.
  https://www.edrdg.org/edrdg/licence.html

**문장 데이터**

- **Tatoeba** — Tatoeba 커뮤니티 기여자 제공.
  Creative Commons Attribution 2.0 France (CC-BY 2.0 FR) 적용.
  https://tatoeba.org/

- **WikiMatrix** — Holger Schwenk 외 (2019). Wikipedia에서 채굴된 병렬 코퍼스.
  Creative Commons Attribution-ShareAlike 4.0 International (CC-BY-SA 4.0) 적용.

- **Project Gutenberg** — 저작권 만료 작품 (1928년 이전 미국).
  퍼블릭 도메인(Public Domain).
  https://www.gutenberg.org/

---

이 앱의 콘텐츠 데이터 중 CC-BY-SA 4.0이 적용되는 부분은 동일한 조건으로 공유됩니다.
앱 코드 및 UI 자산은 저작권자의 독점 소유이며, 별도 허가 없이 복사·배포·변형할 수 없습니다.

---

### 4.3 구현 방식 (권장)

```typescript
// apps/src/components/AttributionScreen.tsx (예시 구조)
// 실제 구현 시 아래 데이터 구조를 상수 파일로 분리하는 것을 권장합니다.

const ATTRIBUTIONS = [
  {
    category: '사전 데이터',
    sources: [
      { name: 'WordNet 3.1', provider: 'Princeton University', license: 'WordNet License', url: 'https://wordnet.princeton.edu/license-and-commercial-use' },
      { name: 'Wiktionary (en/es/ko)', provider: 'Wikimedia Contributors', license: 'CC-BY-SA 4.0', url: 'https://creativecommons.org/licenses/by-sa/4.0/' },
      { name: 'CC-CEDICT', provider: 'MDBG', license: 'CC-BY-SA 4.0', url: 'https://creativecommons.org/licenses/by-sa/4.0/' },
      { name: 'JMdict / EDICT2', provider: 'EDRDG', license: 'CC-BY-SA 4.0', url: 'https://www.edrdg.org/edrdg/licence.html' },
    ],
  },
  {
    category: '문장 데이터',
    sources: [
      { name: 'Tatoeba', provider: 'Tatoeba Contributors', license: 'CC-BY 2.0 FR', url: 'https://tatoeba.org/' },
      { name: 'WikiMatrix', provider: 'Schwenk et al. / OPUS', license: 'CC-BY-SA 4.0', url: 'https://opus.nlpl.eu/WikiMatrix.php' },
      { name: 'Project Gutenberg', provider: 'Public Domain', license: 'Public Domain', url: 'https://www.gutenberg.org/' },
    ],
  },
];
```

---

## 5. 실제 호스팅 위치 (Hosting Location)

콘텐츠 청크는 별도의 공개 GitHub 저장소에 호스팅됩니다.

| 항목 | 값 |
|------|-----|
| 공개 저장소 URL | `https://github.com/GwangHyun-Myung/pingkkukokoLanguage` |
| 콘텐츠 디렉토리 | `content-v1/` |
| 매니페스트 URL | `https://raw.githubusercontent.com/GwangHyun-Myung/pingkkukokoLanguage/main/content-v1/manifest.json` |
| 청크 URL 패턴 | `https://raw.githubusercontent.com/GwangHyun-Myung/pingkkukokoLanguage/main/content-v1/<chunkPath>` |

### 파일 크기 제한

GitHub raw content URL은 단일 파일 최대 100 MB를 제공합니다. 현재 생성된 청크는 최대 11.3 MB (압축)이므로 제한 범위 내에 있습니다.

### 선택적 CDN 대안

```
https://cdn.jsdelivr.net/gh/GwangHyun-Myung/pingkkukokoLanguage@main/content-v1/<path>
```

jsDelivr CDN을 통하면 전 세계적으로 더 빠른 속도를 제공할 수 있습니다. 단, jsDelivr 프록시에 의존하므로 가용성이 GitHub raw에 비해 다를 수 있습니다. 프로덕션 배포 전 상황에 따라 선택하십시오.

---

## 6. 배포 체크리스트 (Distribution Checklist)

출시 전 아래 항목을 모두 완료했는지 확인합니다.

### 5.1 저장소 준비

- [ ] `apps/LICENSE` 생성 (Proprietary License 본문)
- [ ] `tools/LICENSE` 생성 (Proprietary License 본문)
- [ ] `datas/LICENSE` 생성 (CC-BY-SA 4.0 전문 또는 링크)
- [ ] `datas/ATTRIBUTIONS.md` 생성 (전체 업스트림 소스 목록)
- [ ] `tools/data-pipeline/raw/` 가 `.gitignore`에 등록되어 있는지 확인

### 5.2 APK 내 포함

- [ ] 앱 내 저작자 표시(크레딧) 화면 구현 완료
- [ ] 크레딧 화면에서 CC-BY-SA 4.0 라이선스 URL 링크 포함
- [ ] `assets/NOTICES.txt` 또는 동등한 파일 APK에 포함
- [ ] Play Store 앱 설명란(description)에 오픈 데이터 소스 사용 언급

### 5.3 데이터 청크 아카이브

- [ ] 각 `.jsonl.gz` 아카이브 최상위에 `LICENSE.txt` 포함
- [ ] 각 `.jsonl.gz` 아카이브 최상위에 `ATTRIBUTIONS.txt` 포함
- [ ] GitHub Releases 릴리스 설명에 CC-BY-SA 4.0 명시

### 5.4 사이드로드 패키지

- [ ] APK와 함께 배포하는 ZIP/폴더에 `LICENSE.txt` 동봉
- [ ] APK와 함께 배포하는 ZIP/폴더에 `ATTRIBUTIONS.txt` 동봉

---

## 참고 문서

- [[01-license-audit]] — 의존성 라이선스 전수 조사
- [[02-license-compatibility]] — 라이선스 호환성 분류
- [[04-code-rights-protection]] — 자체 코드의 권리 보호
- [[05-proprietary-license]] — Proprietary License 명시
