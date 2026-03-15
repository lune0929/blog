# VS Code JSON 파일 완전 정리

> VS Code의 설정은 여러 JSON 파일로 나뉘어 관리됨.
> **전역(User) 설정**은 내 PC 전체에 적용되고, **작업공간(.vscode) 설정**은 해당 프로젝트에서만 적용.

---

## 🗂️ 전체 파일 구조

```
📁 C:\Users\<user>\AppData\Roaming\Code\User\   ← 전역 설정 (내 PC 전체)
 ├── settings.json          전역 편집기 설정
 ├── keybindings.json       전역 단축키 설정
 └── snippets\              전역 코드 스니펫
     ├── markdown.json
     ├── python.json
     └── *.code-snippets

📁 내프로젝트\.vscode\                           ← 작업공간 설정 (이 프로젝트만)
 ├── settings.json          프로젝트 전용 편집기 설정
 ├── tasks.json             자동화 작업 정의
 ├── launch.json            실행/디버깅 설정
 └── extensions.json        추천 확장 목록
```

### 적용 범위 한눈에 보기

| 파일 | 위치 | 적용 범위 |
|------|------|-----------|
| `User/settings.json` | AppData | 모든 프로젝트 |
| `User/keybindings.json` | AppData | 모든 프로젝트 |
| `User/snippets/*.json` | AppData | 모든 프로젝트 |
| `.vscode/settings.json` | 프로젝트 루트 | 이 프로젝트만 ✅ |
| `.vscode/tasks.json` | 프로젝트 루트 | 이 프로젝트만 ✅ |
| `.vscode/launch.json` | 프로젝트 루트 | 이 프로젝트만 ✅ |
| `.vscode/extensions.json` | 프로젝트 루트 | 이 프로젝트만 ✅ |

---

## 1️⃣ 주요 JSON — `.vscode` 폴더 (프로젝트 전용)

프로젝트 루트의 `.vscode` 폴더 안에 위치. Git에 커밋하면 팀원 전체에 자동 공유.

| 파일 | 역할 | 보안 위험 |
|------|------|-----------|
| [[settings.json]] | 프로젝트 전용 편집기 설정 | 실행 경로 변조 가능 ⚠️ |
| [[tasks.json]] | 빌드·테스트 등 자동화 명령 | 임의 쉘 명령 실행 가능 ⚠️ |
| [[launch.json]] | F5 실행·디버깅 구성 | 임의 프로그램 실행 가능 ⚠️ |

> **보안 참고:** 폴더를 열 때 VS Code가 신뢰 여부를 묻는 이유가 바로 이 3개 파일 때문.
> 출처 불명의 프로젝트를 열 때는 반드시 내용 확인 후 신뢰 허용.

---

## 2️⃣ 기타 JSON — 전역 설정 파일

### 📁 `snippets/*.json` — 코드 스니펫

자주 쓰는 코드 조각을 단축어로 등록해두는 파일. 언어별로 파일이 분리됨.

**위치:**
```
C:\Users\<user>\AppData\Roaming\Code\User\snippets\
 ├── markdown.json
 ├── python.json
 └── javascript.json
```

**예시 — Python 스니펫:**
```json
{
  "Main guard": {
    "prefix": "main",
    "body": [
      "if __name__ == '__main__':",
      "    $0"
    ],
    "description": "Python 진입점 패턴"
  }
}
```

| 항목 | 설명 |
|------|------|
| `prefix` | 단축어 (이 단어 입력 후 Tab) |
| `body` | 삽입될 코드 (`$0`은 커서 위치) |
| `description` | 자동완성 목록에 표시될 설명 |

**전역 vs 프로젝트 스니펫:**

| 구분 | 위치 | 적용 범위 |
|------|------|-----------|
| 전역 스니펫 | `User/snippets/*.json` | 모든 프로젝트 |
| 프로젝트 스니펫 | `.vscode/*.code-snippets` | 이 프로젝트만 |

---

### 🔗 `.vscode/extensions.json` — 추천 확장 목록

팀원에게 이 프로젝트에 필요한 확장을 자동으로 추천해주는 파일.
폴더를 열면 VS Code가 "이 확장을 설치하시겠습니까?" 알림을 표시.

**위치:**
```
내프로젝트\.vscode\extensions.json
```

**예시:**
```json
{
  "recommendations": [
    "ms-python.python",
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint",
    "eamodio.gitlens"
  ]
}
```

> **Tip:** 확장 ID는 확장 프로그램 페이지에서 우클릭 → "확장 ID 복사"로 가져올 수 있음.
> Git에 커밋해두면 새 팀원이 프로젝트를 열자마자 필요한 확장을 한 번에 설치 가능.

---

### ⌨️ `keybindings.json` — 단축키 설정

VS Code 전체의 단축키를 커스터마이징하는 파일. 전역 설정이며 프로젝트별 분리 불가.

**위치:**
```
C:\Users\<user>\AppData\Roaming\Code\User\keybindings.json
```

**예시:**
```json
[
  {
    "key": "ctrl+shift+t",
    "command": "workbench.action.terminal.new"
  },
  {
    "key": "ctrl+k ctrl+d",
    "command": "editor.action.formatDocument",
    "when": "editorTextFocus"
  }
]
```

| 항목 | 설명 |
|------|------|
| `key` | 단축키 조합 |
| `command` | 실행할 VS Code 명령 ID |
| `when` | 이 단축키가 활성화되는 조건 (선택) |

> **Tip:** `Ctrl+Shift+P` → "기본 바로 가기 키 열기(JSON)" 로 현재 모든 단축키 확인 가능.

---

## ✅ 정리 요약

```
🌐 전역 설정 (User 폴더)
   ├── settings.json     →  모든 프로젝트에 적용되는 편집기 설정
   ├── keybindings.json  →  전체 단축키 커스터마이징
   └── snippets/*.json   →  언어별 코드 스니펫

📁 프로젝트 설정 (.vscode 폴더)
   ├── settings.json     →  이 프로젝트 전용 설정 (전역 설정 덮어씀)
   ├── tasks.json        →  빌드·테스트 자동화 명령 등록
   ├── launch.json       →  F5 실행/디버깅 구성
   └── extensions.json   →  팀원에게 추천할 확장 목록
```

---

*작성일: 2026-03-15 | VS Code .vscode 폴더 완전 정리 시리즈*
