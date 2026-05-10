# Phil Notepad+ 사용 설명서

> **Version 1.2** · Python / tkinter 기반 경량 텍스트 에디터

---

## 📋 개요

**Phil Notepad+**는 Notepad++의 핵심 기능을 Python 표준 라이브러리(tkinter)만으로 구현한 경량 텍스트 에디터입니다.

- **외부 패키지 불필요** — Python만 설치되어 있으면 바로 실행 가능
- **단일 파일** — `phil_notepad_plus.py` 하나로 모든 기능 제공
- **EXE 변환 가능** — PyInstaller로 단일 실행 파일 배포 가능
- **세션 자동 저장** — 열었던 파일, 설정 등을 `.tmp` 파일로 저장/복원

---

## 🚀 설치 및 실행

### 스크립트 실행

```bash
python phil_notepad_plus.py
```

> Python 3.7 이상 필요. 추가 패키지 설치 없이 바로 실행됩니다.

### EXE 빌드 (배포용)

```bash
pip install pyinstaller
pyinstaller --onefile --windowed --name "PhilNotepadPlus" phil_notepad_plus.py
```

빌드 결과: `dist/PhilNotepadPlus.exe` → 이 파일만 전달하면 됩니다.

---

## ✨ 주요 기능

### 1. 탭 인터페이스

여러 파일을 동시에 열어 탭으로 전환하며 편집할 수 있습니다.

- 새 탭 생성 (`Ctrl+N`)
- 탭 닫기 (`Ctrl+W`) — 저장 여부 확인 다이얼로그 포함
- 탭 간 이동 (`Ctrl+Tab`)

### 2. 구문 강조 (Syntax Highlighting)

**11개 언어**를 지원하며, 파일 확장자에 따라 자동으로 감지됩니다.

| 언어 | 강조 요소 |
|------|-----------|
| Python | 키워드, 내장 함수, 문자열, 주석, 숫자, 데코레이터 |
| C++ | 키워드, 내장 함수, 전처리기(`#include` 등), 문자열, 주석, 숫자 |
| JavaScript | 키워드, 내장 객체, 문자열(템플릿 리터럴 포함), 주석, 숫자 |
| HTML | 태그, 속성, 문자열, 주석 |
| CSS | 셀렉터, 속성, 문자열, 주석, 숫자(단위 포함) |
| JSON | 키, 값 문자열, 숫자, 키워드(`true`/`false`/`null`) |
| SQL | 키워드, 문자열, 주석, 숫자 |
| Markdown | 제목, 볼드, 이탈릭, 코드 블록, 인라인 코드, 링크, 리스트 |
| YAML | 키, 문자열, 주석, 숫자, 불리언 |
| TOML | 섹션 헤더, 키, 문자열, 주석, 숫자, 불리언 |
| Plain Text | 강조 없음 |

Language 메뉴에서 수동으로 언어를 변경할 수도 있습니다.

### 3. 줄 번호

편집기 왼쪽에 줄 번호가 실시간으로 표시됩니다. 스크롤과 동기화됩니다.

### 4. 찾기 & 바꾸기

- **`Ctrl+F`** : 찾기 다이얼로그
- **`Ctrl+H`** : 찾기 & 바꾸기 다이얼로그
- 기능: Find All, Replace, Replace All
- 옵션: 대소문자 구분 토글

### 5. 다크 / 라이트 테마

| 테마 | 배경색 | 특징 |
|------|--------|------|
| **Dark** (기본) | `#1E1E1E` | VS Code Dark 스타일 |
| **Light** | `#FFFFFF` | 밝은 배경, 가독성 우선 |

`View → Theme` 메뉴에서 전환할 수 있습니다.

### 6. 확대 / 축소 (Zoom)

| 단축키 | 동작 |
|--------|------|
| `Ctrl++` 또는 `Ctrl+=` | 확대 |
| `Ctrl+-` | 축소 |
| `Ctrl+0` | 기본 크기(11pt)로 리셋 |

글꼴 크기 범위: 6pt ~ 40pt

### 7. 줄 바꿈 토글

`View → Toggle Word Wrap` 메뉴로 줄 바꿈을 켜거나 끌 수 있습니다.

- **OFF (기본)** : 가로 스크롤바 표시, 긴 줄 그대로 출력
- **ON** : 창 너비에 맞춰 자동 줄 바꿈

### 8. 줄 이동 (Go to Line)

`Ctrl+G`로 특정 줄 번호로 바로 이동할 수 있습니다.

### 9. 수정 표시기

파일이 수정되면 탭 제목에 `*` 기호가 자동 추가됩니다.

- 수정 전: `main.py`
- 수정 후: ` *main.py `

### 10. 세션 저장 / 복원 (.tmp 파일) 🆕

프로그램을 종료해도 작업 상태가 자동으로 저장됩니다.

**저장 시점:**

- 프로그램 종료 시 (창 닫기 / File → Exit)
- 파일 저장 시 (`Ctrl+S`, `Ctrl+Shift+S`)
- 탭 닫기 시 (`Ctrl+W`)

**복원 시점:**

- 프로그램 시작 시 자동으로 `.tmp` 파일을 읽어 복원

**저장 항목:**

| 항목 | 설명 |
|------|------|
| `open_tabs` | 열려 있던 파일 경로, 언어, 커서 위치, 스크롤 위치 |
| `active_tab_index` | 마지막으로 활성화된 탭 번호 |
| `recent_files` | 최근 열었던 파일 목록 (최대 20개) |
| `window_geometry` | 창 크기 및 위치 |
| `theme_name` | 적용 중이던 테마 (Dark / Light) |
| `font_size` | 확대/축소 레벨 |
| `word_wrap` | 줄 바꿈 설정 |
| `last_saved` | 세션 저장 시각 |

> ⚠️ Untitled(저장하지 않은) 탭은 세션에 포함되지 않습니다.

### 11. 최근 파일 목록

`File → Recent Files`에서 최근 열었던 파일을 최대 20개까지 확인하고 바로 열 수 있습니다.

### 12. 우클릭 컨텍스트 메뉴

편집 영역에서 마우스 오른쪽 버튼을 클릭하면:

- Cut / Copy / Paste
- Select All
- Delete

---

## ⌨️ 키보드 단축키 전체 목록

| 단축키 | 동작 |
|--------|------|
| `Ctrl+N` | 새 파일 |
| `Ctrl+O` | 파일 열기 |
| `Ctrl+S` | 저장 |
| `Ctrl+Shift+S` | 다른 이름으로 저장 |
| `Ctrl+W` | 현재 탭 닫기 |
| `Ctrl+Z` | 실행 취소 (Undo) |
| `Ctrl+Y` | 다시 실행 (Redo) |
| `Ctrl+X` | 잘라내기 |
| `Ctrl+C` | 복사 |
| `Ctrl+V` | 붙여넣기 |
| `Ctrl+A` | 전체 선택 |
| `Ctrl+D` | 현재 줄 복제 |
| `Ctrl+F` | 찾기 |
| `Ctrl+H` | 찾기 & 바꾸기 |
| `Ctrl+G` | 줄 이동 |
| `Ctrl+Tab` | 다음 탭으로 이동 |
| `Ctrl++` / `Ctrl+=` | 확대 |
| `Ctrl+-` | 축소 |
| `Ctrl+0` | 줌 리셋 |

---

## 📂 지원 언어 및 확장자 매핑

| 언어 | 확장자 |
|------|--------|
| Python | `.py`, `.pyw` |
| C++ | `.cpp`, `.cxx`, `.cc`, `.c`, `.h`, `.hpp` |
| JavaScript | `.js`, `.mjs`, `.jsx`, `.ts`, `.tsx` |
| HTML | `.html`, `.htm`, `.xml`, `.svg` |
| CSS | `.css`, `.scss`, `.less` |
| JSON | `.json` |
| SQL | `.sql` |
| Markdown | `.md`, `.markdown` |
| YAML | `.yaml`, `.yml` |
| TOML | `.toml` |
| Plain Text | 기타 모든 확장자 |

---

## 💾 세션 파일 (.tmp) 상세

### 파일 위치

```
스크립트 실행 시:  phil_notepad_plus.py 와 같은 폴더
EXE 실행 시:      PhilNotepadPlus.exe 와 같은 폴더
```

파일명: `phil_notepad_plus.tmp`

### 파일 형식

JSON 형식으로 저장되며, 텍스트 에디터로 직접 확인/편집 가능합니다.

```json
{
  "recent_files": [
    "C:/Projects/main.py",
    "C:/Projects/config.yaml"
  ],
  "open_tabs": [
    {
      "filepath": "C:/Projects/main.py",
      "language": "Python",
      "cursor": "15.4",
      "scroll": 0.23
    }
  ],
  "active_tab_index": 0,
  "window_geometry": "1100x720+100+50",
  "theme_name": "Dark",
  "font_size": 12,
  "word_wrap": false,
  "last_saved": "2026-05-08 15:30:45"
}
```

### 저장 시점

| 이벤트 | 세션 저장 |
|--------|-----------|
| 창 닫기 (X 버튼 / File → Exit) | ✅ |
| 파일 저장 (Ctrl+S) | ✅ |
| 다른 이름으로 저장 (Ctrl+Shift+S) | ✅ |
| 탭 닫기 (Ctrl+W) | ✅ |

### 안전장치

- `.tmp` 파일이 손상되어도 프로그램이 정상 실행됩니다 (Welcome 탭 표시)
- 존재하지 않는 파일 경로는 자동으로 무시됩니다
- 모든 읽기/쓰기 작업은 try/except로 보호됩니다

---

## 🎨 테마 색상표

### Dark 테마 (기본)

| 요소 | 색상 |
|------|------|
| 배경 | `#1E1E1E` |
| 텍스트 | `#D4D4D4` |
| 키워드 | `#569CD6` (파란색) |
| 문자열 | `#CE9178` (주황색) |
| 주석 | `#6A9955` (녹색) |
| 숫자 | `#B5CEA8` (연녹색) |
| 내장함수 | `#DCDCAA` (노란색) |
| 전처리기 | `#C586C0` (보라색) |
| 상태표시줄 | `#007ACC` (파란색) |

### Light 테마

| 요소 | 색상 |
|------|------|
| 배경 | `#FFFFFF` |
| 텍스트 | `#000000` |
| 키워드 | `#0000FF` (파란색) |
| 문자열 | `#A31515` (빨간색) |
| 주석 | `#008000` (녹색) |
| 숫자 | `#098658` (청록색) |
| 내장함수 | `#795E26` (갈색) |
| 전처리기 | `#AF00DB` (보라색) |
| 상태표시줄 | `#007ACC` (파란색) |

---

## 📦 EXE 빌드 방법

### 기본 빌드

```bash
pip install pyinstaller
pyinstaller --onefile --windowed --name "PhilNotepadPlus" phil_notepad_plus.py
```

### 아이콘 포함 빌드

```bash
pyinstaller --onefile --windowed --icon=app_icon.ico --name "PhilNotepadPlus" phil_notepad_plus.py
```

### 빌드 결과

```
프로젝트 폴더/
├── dist/
│   └── PhilNotepadPlus.exe   ← 배포할 파일
├── build/                     ← 삭제 가능
└── PhilNotepadPlus.spec       ← 삭제 가능
```

### 참고 사항

| 항목 | 내용 |
|------|------|
| 파일 크기 | 약 8~15 MB (tkinter만 사용하므로 경량) |
| 빌드 환경 | Windows에서 빌드 → `.exe` 생성 |
| 백신 오탐 | PyInstaller EXE는 일부 백신이 오탐할 수 있음. 사내 배포 시 화이트리스트 등록 권장 |
| 세션 파일 | EXE와 같은 폴더에 `phil_notepad_plus.tmp` 자동 생성 |

---

## 📝 메뉴 구조

```
File
├── New              Ctrl+N
├── Open…            Ctrl+O
├── Save             Ctrl+S
├── Save As…         Ctrl+Shift+S
├── Close Tab        Ctrl+W
├── Recent Files     →
└── Exit

Edit
├── Undo             Ctrl+Z
├── Redo             Ctrl+Y
├── Cut              Ctrl+X
├── Copy             Ctrl+C
├── Paste            Ctrl+V
├── Select All       Ctrl+A
└── Duplicate Line   Ctrl+D

Search
├── Find…            Ctrl+F
├── Replace…         Ctrl+H
└── Go to Line…      Ctrl+G

View
├── Zoom In          Ctrl++
├── Zoom Out         Ctrl+-
├── Reset Zoom       Ctrl+0
├── Toggle Word Wrap
└── Theme → Dark / Light

Language
├── Python
├── C++
├── JavaScript
├── HTML
├── CSS
├── JSON
├── SQL
├── Markdown
├── YAML
├── TOML
└── Plain Text

Help
└── About
```

---

## ℹ️ 버전 정보

| 항목 | 내용 |
|------|------|
| 프로그램명 | Phil Notepad+ |
| 버전 | 1.2 |
| 언어 | Python 3.7+ |
| GUI | tkinter (표준 라이브러리) |
| 라이선스 | 자유 사용 |
| © | 2026 |

---

*이 문서는 Phil Notepad+ v1.2 기준으로 작성되었습니다.*
