# SRS — Hancomins Helper 개인정보처리방침 페이지

> 본 문서는 IEEE/ISO/IEC 29148:2018 (Systems and software engineering — Life cycle processes — Requirements engineering) 의 SRS 구조를 따른다.

| 항목 | 값 |
|---|---|
| 문서 ID | SRS-HHP-001 |
| 버전 | 1.0 |
| 작성일 | 2026-06-15 |
| 상태 | 승인 |
| 대상 시스템 | echoes-policy (GitHub Pages, `echoesdiary.co.kr`) |

---

## 1. 개요 (Introduction)

### 1.1 목적 (Purpose)
사내 업무 보조 Chrome 확장 프로그램 "Hancomins Helper" 의 개인정보처리방침을 공개 URL 로 게시하기 위한 정적 웹 페이지의 요구사항을 정의한다. 본 페이지는 Chrome 웹스토어 등록 시 요구되는 개인정보처리방침 URL 요건을 충족하기 위해 작성된다.

### 1.2 범위 (Scope)
- **포함**: 기존 정적 호스팅 repo(`echoes-policy`)에 단일 HTML 페이지 1개 추가, 기존 디자인 스타일 재사용.
- **제외**: Hancomins Helper 확장 자체의 기능, 백엔드 연동, 기존 Echoes 페이지(`index.html`, `privacy.html`) 변경.

### 1.3 정의·약어 (Definitions and Acronyms)
| 용어 | 설명 |
|---|---|
| Hancomins Helper | 사내 업무 보조용 Chrome 확장 프로그램 |
| `chrome.storage.local` | 확장이 사용자 브라우저 로컬에 데이터를 저장하는 Chrome API |
| GitHub Pages | 정적 페이지 호스팅 서비스 (본 repo 배포 수단) |

### 1.4 참조 (References)
- ISO/IEC/IEEE 29148:2018
- 기존 페이지: `privacy.html` (Echoes 개인정보처리방침) — 스타일·명명 규칙 기준
- 배포: `CNAME` = `echoesdiary.co.kr`

---

## 2. 전체 설명 (Overall Description)

### 2.1 제품 관점 (Product Perspective)
`echoes-policy` repo 는 GitHub Pages 로 `echoesdiary.co.kr` 도메인에 배포되는 정적 사이트다. 본 페이지는 해당 사이트에 독립 경로로 추가되는 정적 HTML 1개이며 별도 빌드·런타임 의존성이 없다.

### 2.2 사용자 특성 (User Characteristics)
- Hancomins Helper 설치/검토자(사내 직원, 웹스토어 심사자).
- 별도 인증 없이 누구나 URL 로 열람 가능.

### 2.3 제약 (Constraints)
- 정적 HTML 만 사용(서버 로직 없음).
- 기존 `privacy.html` 의 CSS·레이아웃 스타일을 따른다.
- 한국어(`lang="ko"`) 기준.

### 2.4 가정·의존성 (Assumptions and Dependencies)
- GitHub Pages 배포 및 `echoesdiary.co.kr` DNS·HTTPS 가 정상 동작 중(DEC-039 기준).
- push 후 GitHub Pages 자동 배포로 페이지가 공개된다.

---

## 3. 구체적 요구사항 (Specific Requirements)

### 3.1 기능 요구사항 (Functional Requirements)
| ID | 요구사항 |
|---|---|
| FR-1 | 페이지는 `hancomins-helper-privacy.html` 경로로 추가되어 `https://echoesdiary.co.kr/hancomins-helper-privacy.html` 에서 접근 가능해야 한다. |
| FR-2 | 제목은 "Hancomins Helper 개인정보처리방침" 이어야 한다. |
| FR-3 | 다음 5개 항목을 순서대로 포함해야 한다: (1) 수집·저장 정보, (2) 외부 전송, (3) 제3자 제공, (4) 사용 목적, (5) 문의. |
| FR-4 | 수집·저장 정보 항목은 사용자 입력 설정(Redmine 주소·API Key)·체크리스트·고객사 메모·템플릿이 `chrome.storage.local` 로컬 저장소에만 보관됨을 명시해야 한다. |
| FR-5 | 외부 전송 항목은 데이터를 외부 서버로 전송하지 않으며, 사내 시스템 통신은 사용자가 직접 실행한 동작에 한정되고 화면 원문·개인정보를 임의 전송하지 않음을 명시해야 한다. |
| FR-6 | 제3자 제공은 "없음", 사용 목적은 "사내 업무 보조 기능 제공", 문의는 "010-9551-3290" 로 명시해야 한다. |

### 3.2 외부 인터페이스 요구사항 (External Interface Requirements)
| ID | 요구사항 |
|---|---|
| EIR-1 | 입력: HTTP GET 요청. 출력: HTML 문서(text/html). |
| EIR-2 | 별도 API·DB·인증 인터페이스를 갖지 않는다. |

### 3.3 품질 요구사항 (Quality / Non-functional Requirements)
| ID | 요구사항 |
|---|---|
| NFR-1 | 모바일·데스크톱 반응형(viewport meta + `max-width`)을 지원해야 한다. |
| NFR-2 | 기존 `privacy.html` 과 시각적으로 일관(폰트·색상 #4A7BD8·레이아웃)되어야 한다. |
| NFR-3 | 외부 스크립트·추적기를 포함하지 않는다. |
| NFR-4 | 사내용 페이지로 검색 노출을 막기 위해 `noindex` 메타를 포함한다. |

---

## 4. 검증 (Verification)
| 대상 | 방법 | 기준 |
|---|---|---|
| FR-1 | push 후 URL 접속 | HTTP 200, 페이지 렌더링 |
| FR-2~FR-6 | 페이지 본문 육안 확인 | 5개 항목·문구 일치 |
| NFR-1 | 브라우저 폭 변경 | 레이아웃 정상 |
| NFR-2 | `privacy.html` 과 비교 | 스타일 일관 |

---

## 5. 추적성 (Traceability)
| 요구사항 | 산출물 |
|---|---|
| FR-1~FR-6, NFR-1~NFR-4 | `hancomins-helper-privacy.html` |
