# `.vscode/settings.json` — 프로젝트 전용 편집기 설정

> VS Code의 설정은 **두 층**으로 나뉨.
> 전역(Global) 설정은 모든 프로젝트에 적용되고, `.vscode/settings.json`은 **이 폴더에서만** 작동하는 설정을 덮어씀.

---

## 💡 한 줄 요약

> **"이 프로젝트를 열었을 때, VS Code가 어떻게 동작할지"를 정의하는 파일.**

---

## 🗂️ 위치와 적용 범위

```
프로젝트 루트/
└── .vscode/
    └── settings.json   ← 여기
```

| 설정 종류 | 파일 위치 | 적용 범위 |
|-----------|----------|-----------|
| 전역 설정 | `%APPDATA%\Code\User\settings.json` | 모든 프로젝트 |
| 작업공간 설정 | `.vscode/settings.json` | 이 폴더만 ✅ |

> **우선순위:** 작업공간 설정 > 전역 설정. 같은 키가 있으면 작업공간 설정이 이김.

---

## 🔤 기본 예시

```json
{
  "editor.formatOnSave": true,
  "editor.tabSize": 2,
  "python.defaultInterpreterPath": ".venv/Scripts/python.exe"
}
```

| 키 | 값 | 효과 |
|----|----|------|
| `editor.formatOnSave` | `true` | 저장 시 코드 자동 정렬 |
| `editor.tabSize` | `2` | 탭 크기를 2칸으로 고정 |
| `python.defaultInterpreterPath` | 경로 | 이 프로젝트에서 쓸 Python 인터프리터 지정 |

---

## 📋 자주 쓰이는 설정 모음

### 에디터 기본

```json
{
  "editor.formatOnSave": true,
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "editor.wordWrap": "on",
  "editor.rulers": [80, 120],
  "files.trimTrailingWhitespace": true,
  "files.insertFinalNewline": true
}
```

### Python 프로젝트

```json
{
  "python.defaultInterpreterPath": ".venv/Scripts/python.exe",
  "python.linting.enabled": true,
  "python.linting.pylintEnabled": true,
  "editor.formatOnSave": true,
  "[python]": {
    "editor.defaultFormatter": "ms-python.black-formatter"
  }
}
```

### JavaScript / Node.js 프로젝트

```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "eslint.enable": true,
  "[javascript]": {
    "editor.tabSize": 2
  },
  "typescript.preferences.importModuleSpecifier": "relative"
}
```

### 언어별 설정 분리 (`[언어명]` 키)

같은 프로젝트에서 언어마다 다른 규칙을 적용할 때 사용.

```json
{
  "editor.tabSize": 4,
  "[python]": {
    "editor.tabSize": 4
  },
  "[javascript]": {
    "editor.tabSize": 2
  },
  "[markdown]": {
    "editor.wordWrap": "on",
    "editor.quickSuggestions": false
  }
}
```

---

## 🔒 왜 VS Code가 보안 경고를 띄우나

폴더를 열 때 이런 경고가 나타나는 이유가 바로 이 파일 때문.

```
⚠️ "이 폴더의 파일을 신뢰하시겠습니까?"
```

`settings.json`은 단순히 텍스트를 보여주는 파일이 아님. 폴더를 여는 순간 **즉시 자동 적용**됨.

| 단순 파일 열기 | 폴더(프로젝트) 열기 |
|--------------|-------------------|
| 내용만 표시 | `.vscode/settings.json` 자동 로드 |
| 아무 동작 없음 | 편집기 동작 방식 즉시 변경 |
| — | 확장 기능 동작 방식도 변경됨 |

### 악용 가능한 시나리오

```json
{
  "python.defaultInterpreterPath": "C:/malware/fake_python.exe"
}
```

악의적인 `settings.json`이 있으면, 프로젝트를 여는 순간 전혀 다른 실행 파일이 Python으로 등록됨.
이후 코드를 실행하면 악성 프로그램이 대신 동작.

→ 출처를 모르는 프로젝트 폴더는 열지 않는 것이 원칙.

---

## ⚙️ 실무 활용 패턴

### 팀 공유 설정

`.vscode/settings.json`을 Git에 커밋하면 팀원 전체가 동일한 편집 규칙을 자동 적용.
코드 스타일 통일에 효과적.

```json
{
  "editor.formatOnSave": true,
  "editor.tabSize": 2,
  "files.eol": "\n",
  "files.trimTrailingWhitespace": true
}
```

### 개인 설정 제외

개인 취향 설정은 팀과 공유하면 안 됨. `.gitignore`에 추가.

```gitignore
# 개인 설정은 제외
.vscode/settings.json

# 팀 공유 설정은 포함 (선택적)
!.vscode/extensions.json
```

---

## ✅ 정리 요약

```
📍 위치       →  .vscode/settings.json
🎯 역할       →  이 프로젝트 전용 편집기 설정
⚡ 작동 시점   →  폴더를 여는 순간 즉시 적용
🏆 우선순위   →  전역 설정보다 높음
🔒 보안 주의  →  신뢰하지 않는 폴더의 파일은 검토 필수
```

---

*작성일: 2026-03-15 | VS Code .vscode 폴더 완전 정리 시리즈*
