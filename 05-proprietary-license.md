---
date: 2026-05-03
type: legal-policy
step: 5
related: [[01-license-audit]], [[02-license-compatibility]], [[03-distribution-structure]], [[04-code-rights-protection]]
---

# 05 — Proprietary License 명시 (Proprietary License Declaration)

> **면책 고지**: 이 문서는 프로젝트 내부 참고용 자료이며 법적 조언(legal advice)이 아닙니다. 라이선스 본문의 최종 확정 및 법적 효력 검토는 반드시 자격을 갖춘 변호사(attorney)에게 의뢰하십시오.

---

## 1. 라이선스 모델 선택 (License Model Selection)

### 1.1 검토한 옵션

| 모델 | 설명 | 권장 여부 |
|------|------|---------|
| **All Rights Reserved (전체 권리 보유)** | 소스 코드 비공개, 모든 권리 저작권자 보유. 무단 복사·배포·수정 전면 금지. | **권장** ✅ |
| **Business Source License (BSL/BUSL)** | 소스 공개하되 일정 기간 동안 상업적 이용 제한. 일정 기간 후 오픈소스 전환. | 나중에 고려 가능 |
| **Closed Binary Distribution Only** | 바이너리(APK)만 배포, 소스 비공개. All Rights Reserved의 배포 방식 변형. | 현행 APK 배포와 동일 |
| **Source Available (열람 전용)** | 소스는 공개하되 복사·배포·상업 이용 금지. | 선택 가능 (BSL 유사) |

### 1.2 권장 모델: All Rights Reserved

pingkkukoko는 다음 이유로 **All Rights Reserved** 모델을 권장합니다.

1. **CC 데이터 레이어와의 명확한 분리**: 앱 코드는 독점으로 보호하고, 데이터만 CC-BY-SA 4.0으로 공유하는 명확한 이중 레이어(dual-layer) 구조를 실현합니다.
2. **경쟁사 복제 방지**: 앱 아키텍처, 게이미피케이션 로직, UX 설계가 경쟁사에 노출되지 않습니다.
3. **라이선스 변경 유연성**: 나중에 BSL, MIT 등으로 전환하는 것은 항상 가능하지만, 반대(오픈소스 → 독점)는 이미 배포된 버전에는 적용이 불가능합니다. 보수적으로 시작하는 것이 안전합니다.
4. **CC 라이선스 의무 미충돌**: All Rights Reserved 코드는 CC-BY-SA 데이터와 집합저작물(mere aggregation)로 공존 가능합니다. `[[02-license-compatibility]]` 참조.

---

## 2. 독점 LICENSE 파일 본문 초안

아래는 `apps/LICENSE` 및 `tools/LICENSE`에 사용할 독점 라이선스 본문 초안입니다. `<COPYRIGHT_HOLDER>`, `<YEAR>` 항목을 실제 값으로 교체하여 사용하십시오.

---

```
PINGKKUKOKO PROPRIETARY SOFTWARE LICENSE

Copyright (c) <YEAR> <COPYRIGHT_HOLDER>. All Rights Reserved.

pingkkukoko 독점 소프트웨어 라이선스

저작권 (c) <YEAR> <COPYRIGHT_HOLDER>. 전체 권리 보유.

------------------------------------------------------------------

1. 정의 (Definitions)

"소프트웨어(Software)"란 이 라이선스가 첨부된 모든 소스 코드, 
오브젝트 코드, 빌드 스크립트, 설정 파일, 문서, 및 관련 자료를 
의미합니다.

"저작권자(Copyright Holder)"란 위에 명시된 <COPYRIGHT_HOLDER>를 
의미합니다.

"사용자(User)"란 이 소프트웨어를 설치하거나 사용하는 개인 또는 
법인을 의미합니다.

2. 허가 범위 (Permitted Uses)

저작권자는 최종 사용자에게 다음의 제한된 권리를 부여합니다.

(a) 컴파일된 바이너리(APK) 형태의 소프트웨어를 개인 기기에 
    설치하고 실행할 권리.
(b) 개인적, 비상업적 목적으로 소프트웨어를 사용할 권리.

3. 금지 행위 (Prohibited Uses)

다음 행위는 사전 서면 허가 없이 엄격히 금지됩니다.

(a) 소프트웨어의 소스 코드, 오브젝트 코드, 또는 이에 파생된 
    형태를 복사, 게시, 배포하는 행위.
(b) 소프트웨어를 수정, 번역, 개작하거나 2차적저작물을 
    작성하는 행위.
(c) 소프트웨어를 리버스 엔지니어링(reverse engineering), 
    역컴파일(decompile), 역어셈블(disassemble)하는 행위.
(d) 소프트웨어를 상업적 목적으로 사용하거나 제3자에게 
    서비스로 제공하는 행위.
(e) 소프트웨어에 포함된 저작권 고지(copyright notice), 
    라이선스 고지, 또는 제한 사항 문구를 제거하거나 
    변경하는 행위.
(f) 소프트웨어를 복제하여 별도의 앱, 서비스, 또는 제품을 
    만들거나 그 기반으로 사용하는 행위.

4. 데이터 레이어 별도 고지 (Data Layer Notice)

이 소프트웨어는 별도의 라이선스(Creative Commons 
Attribution-ShareAlike 4.0 International, "CC-BY-SA 4.0")가 
적용되는 언어 학습 데이터를 포함하거나 참조합니다. 이 데이터는 
소프트웨어 코드와 구분되는 별도의 저작물로서, 해당 데이터에 
대한 권리와 의무는 CC-BY-SA 4.0에 따릅니다. 이 독점 라이선스는 
CC-BY-SA 4.0이 적용되는 데이터 부분에는 적용되지 않습니다.

CC-BY-SA 4.0 데이터 출처 및 저작자 표시:
이 앱 내 설정 화면 또는 정보 화면의 "데이터 출처" 항목을 
참조하십시오.

5. 보증 면책 (Disclaimer of Warranties)

이 소프트웨어는 "있는 그대로(AS IS)" 제공됩니다. 저작권자는 
상품성, 특정 목적 적합성, 또는 비침해에 관한 묵시적 보증을 
포함하여 어떠한 명시적 또는 묵시적 보증도 하지 않습니다.

6. 책임 제한 (Limitation of Liability)

저작권자는 이 소프트웨어의 사용 또는 사용 불능으로 인해 발생하는 
직접적, 간접적, 부수적, 특별, 징벌적, 또는 결과적 손해에 대해 
어떠한 경우에도 책임을 지지 않습니다.

7. 준거법 (Governing Law)

이 라이선스는 대한민국 법률에 따라 해석되고 집행됩니다.

8. 문의

라이선스 허가 요청 또는 문의는 아래로 연락하십시오.
<COPYRIGHT_HOLDER>
prozect@hanmail.net

------------------------------------------------------------------

ENGLISH SUMMARY

All Rights Reserved. No part of this software — including source 
code, compiled binaries, build scripts, configuration, and 
associated documentation — may be copied, distributed, modified, 
reverse-engineered, or used to create derivative works without 
the prior written permission of the copyright holder.

End users are granted the limited right to install and run the 
compiled application (APK) on their personal devices for 
personal, non-commercial use only.

The language learning data bundled with or downloaded by this 
application is separately licensed under CC-BY-SA 4.0 and is 
not covered by this proprietary license. See the in-app 
attribution screen for details.
```

---

## 3. 독점 라이선스 적용 범위 (Scope of Proprietary License)

### 3.1 적용 대상 (Covered by Proprietary License)

| 항목 | 경로 |
|------|------|
| 앱 소스 코드 전체 | `apps/src/` |
| Expo Router 라우트 코드 | `apps/app/` |
| 빌드 설정 및 구성 파일 | `apps/app.json`, `apps/eas.json`, `apps/package.json` 등 |
| UI 자산 (이미지, 아이콘, 폰트 — 서드파티 라이선스 제외) | `apps/assets/` |
| 데이터 파이프라인 소스 코드 | `tools/data-pipeline/src/` |
| 이 문서 세트 (`datas/*.md`) | `datas/` |

### 3.2 적용 제외 대상 (Not Covered — Separate Licenses Apply)

| 항목 | 경로 | 적용 라이선스 |
|------|------|-------------|
| 번들 코어 데이터 (10개 레코드) | `apps/src/data/<lang>/unit*.json` | CC-BY-SA 4.0 |
| 전체 콘텐츠 청크 아카이브 | `datas/content-v1/*.jsonl.gz` | CC-BY-SA 4.0 |
| 앱 런타임 의존성 (node_modules) | — | 각 패키지별 (MIT, Apache 등) |
| 빌드 도구 의존성 | — | MIT, ISC, Apache-2.0 |

---

## 4. 최종 사용자 허가 범위 (Permitted Uses — End User)

최종 사용자가 명시적 허가 없이 수행할 수 있는 행위:

- ✅ Play Store 또는 공식 배포 채널을 통해 앱을 다운로드하고 설치
- ✅ 개인 기기에서 학습 목적으로 앱 사용
- ✅ 앱의 학습 진행 데이터를 자신의 기기에 저장 (오프라인 우선 아키텍처)
- ✅ 앱 스크린샷을 개인적·비상업적 목적(SNS 공유 등)으로 촬영

최종 사용자가 명시적 허가 없이 수행할 수 없는 행위:

- ❌ APK를 추출하거나 재배포
- ❌ 앱 코드를 리버스 엔지니어링
- ❌ 앱 코드를 기반으로 파생 앱 제작
- ❌ 앱을 상업적 목적으로 사용하거나 제3자에게 서비스 제공

---

## 5. 라이선스 집행 및 앱 내 고지 (License Enforcement and In-App Display)

### 5.1 APK 배포는 저작권 포기가 아님

APK를 Play Store에 게시하거나 직접 배포하는 행위 자체는 소스 코드에 대한 저작권을 포기(waiver)하는 것이 아닙니다. 저작권은 창작 즉시 자동으로 발생하며, 배포 방식과 무관하게 유지됩니다.

### 5.2 앱 내 라이선스 고지

사용자가 앱의 라이선스 조건을 인지할 수 있도록, 앱의 설정(Settings) 또는 정보(About) 화면에 다음 내용을 포함하는 것을 권장합니다.

```
이용약관 및 라이선스 안내

pingkkukoko 앱 및 그 소스 코드, UI 자산은 <COPYRIGHT_HOLDER>의 
독점 저작물이며, 무단 복사·배포·수정을 금합니다.

앱에 포함된 언어 학습 데이터는 Creative Commons Attribution-
ShareAlike 4.0 International 라이선스 하의 공개 소스에서 
파생되었습니다. 데이터 출처 및 저작자 표시는 아래 "데이터 출처" 
항목을 확인하십시오.

[이용약관 전문 보기]  [데이터 출처 보기]
```

### 5.3 Google Play 정책 준수

Google Play의 배포 조건은 핑크쿠코코의 독점 라이선스 조건에 추가적으로 적용됩니다. Play Developer Distribution Agreement(DDA)는 Google에 앱 배포권을 부여하지만, 이것이 최종 사용자나 제3자에게 소스 코드 권리를 부여하지는 않습니다.

---

## 참고 문서

- [[01-license-audit]] — 의존성 라이선스 전수 조사
- [[02-license-compatibility]] — 라이선스 호환성 분류
- [[03-distribution-structure]] — 저장소 및 배포물 구성
- [[04-code-rights-protection]] — 자체 코드의 권리 보호
