---
date: 2026-05-04
type: legal-policy
step: 3
related: [[01-license-audit]], [[02-license-compatibility]], [[04-code-rights-protection]], [[05-proprietary-license]]
---

# 03 — 데이터 배포물 구성 (Data Distribution Structure)

> **면책 고지**: 이 문서는 프로젝트 내부 참고용 자료이며 법적 조언(legal advice)이 아닙니다. 배포 전 자격을 갖춘 변호사(attorney)의 검토를 권장합니다.

이 문서는 `datas/` 디렉토리 내 콘텐츠 청크 배포만 다룹니다. 앱 코드 측 배포(Play Store APK, 앱 내 저작자 표시 화면 등)는 `../apps/03-distribution-structure.md` 참조.

---

## 1. 개요

이 문서는 `datas/` 레이어의 라이선스 준수(license compliance)를 실현하기 위한 파일 구조와 배포 산출물(distribution artifact)의 구성 방식을 정의합니다. `[[02-license-compatibility]]`에서 도출한 CC-BY-SA 4.0 분류를 실제 디렉토리 구조와 청크 아카이브 배포 패키지에 어떻게 반영할지를 명시합니다.

---

## 2. `datas/` 디렉토리 구조 (Repository Structure)

### 2.1 `datas/` 서브트리

```
datas/                           ← CC 파생 데이터 레이어
├── LICENSE                      ← [생성 예정] CC-BY-SA 4.0 전문
├── ATTRIBUTIONS.md              ← [생성 예정] 모든 업스트림 소스 표시
├── content-v1/                  ← 청크 아카이브 (다운로드 대상)
│   ├── manifest.json            ← 청크 목록 및 메타데이터
│   ├── en-words-001.jsonl.gz
│   ├── zh-words-001.jsonl.gz
│   └── ...
├── 01-license-audit.md
├── 02-license-compatibility.md
├── 03-distribution-structure.md
├── 04-code-rights-protection.md
└── 05-proprietary-license.md
```

### 2.2 `datas/` LICENSE 파일 배치

| 파일 | 내용 | 상태 |
|------|------|------|
| `datas/LICENSE` | CC-BY-SA 4.0 전문 (Creative Commons Corporation 공식 텍스트 링크 포함) | 생성 예정 |
| `datas/ATTRIBUTIONS.md` | 모든 업스트림 소스 저작자 표시 목록 | 생성 예정 |

> **참고**: 위 파일들은 이 문서 세트가 확정된 후 별도로 생성합니다. 현 시점에서는 이 문서(`03-distribution-structure.md`)가 각 파일의 내용 기준(reference specification)으로 기능합니다.

---

## 3. 콘텐츠 청크 아카이브 (URL 호스팅)

`datas/content-v1/*.jsonl.gz` 파일을 GitHub Releases 또는 외부 CDN에 호스팅하는 경우, 각 아카이브 자체에 라이선스 정보를 포함해야 합니다.

### 옵션 A — 아카이브 내 포함 (권장)

각 `.jsonl.gz` 파일을 압축 해제하면 최상위에 다음 파일이 존재하도록 구성합니다:

```
en-words-001/
├── LICENSE.txt         ← CC-BY-SA 4.0 전문
├── ATTRIBUTIONS.txt    ← 원천 소스 목록
└── data.jsonl          ← 실제 데이터
```

### 옵션 B — 매니페스트 페치 (Manifest Fetch) 방식

앱이 첫 실행 시 청크 목록과 함께 라이선스 메타데이터 URL을 서버에서 수신합니다. 라이선스 본문은 별도 URL로 제공하고, 앱 크레딧 화면에서 이를 참조합니다.

> **권장**: 옵션 A가 아카이브 자체에 라이선스를 포함시키므로, 파일이 재배포되더라도 라이선스 정보가 분리되지 않아 더 안전합니다.

---

## 4. 실제 호스팅 위치 (Hosting Location)

콘텐츠 청크는 별도의 공개 GitHub 저장소에 호스팅됩니다.

| 항목 | 값 |
|------|-----|
| 공개 저장소 URL | `https://github.com/GwangHyun-Myung/pingkkukokoLanguage` |
| 기본 브랜치 | `mbase` |
| 콘텐츠 디렉토리 | `content-v1/` |
| 매니페스트 URL | `https://raw.githubusercontent.com/GwangHyun-Myung/pingkkukokoLanguage/mbase/content-v1/manifest.json` |
| 청크 URL 패턴 | `https://raw.githubusercontent.com/GwangHyun-Myung/pingkkukokoLanguage/mbase/content-v1/<chunkPath>` |

### 파일 크기 제한

GitHub raw content URL은 단일 파일 최대 100 MB를 제공합니다. 현재 생성된 청크는 최대 11.3 MB (압축)이므로 제한 범위 내에 있습니다.

### 선택적 CDN 대안

```
https://cdn.jsdelivr.net/gh/GwangHyun-Myung/pingkkukokoLanguage@mbase/content-v1/<path>
```

jsDelivr CDN을 통하면 전 세계적으로 더 빠른 속도를 제공할 수 있습니다. 단, jsDelivr 프록시에 의존하므로 가용성이 GitHub raw에 비해 다를 수 있습니다. 프로덕션 배포 전 상황에 따라 선택하십시오.

---

## 5. 배포 체크리스트 (Distribution Checklist)

출시 전 아래 항목을 모두 완료했는지 확인합니다.

### 5.1 저장소 준비

- [ ] `datas/LICENSE` 생성 (CC-BY-SA 4.0 전문 또는 공식 링크)
- [ ] `datas/ATTRIBUTIONS.md` 생성 (전체 업스트림 소스 목록)
- [ ] `raw/` 원본 덤프 캐시 디렉토리가 `.gitignore`에 등록되어 있는지 확인

### 5.2 데이터 청크 아카이브

- [ ] 각 `.jsonl.gz` 아카이브 최상위에 `LICENSE.txt` 포함
- [ ] 각 `.jsonl.gz` 아카이브 최상위에 `ATTRIBUTIONS.txt` 포함
- [ ] GitHub Releases 릴리스 설명에 CC-BY-SA 4.0 명시
- [ ] 매니페스트(`manifest.json`)에 라이선스 메타데이터 필드 포함

---

## 참고 문서

- [[01-license-audit]] — 의존성 라이선스 전수 조사
- [[02-license-compatibility]] — 라이선스 호환성 분류
- [[04-code-rights-protection]] — 자체 코드의 권리 보호
- [[05-proprietary-license]] — Proprietary License 명시
