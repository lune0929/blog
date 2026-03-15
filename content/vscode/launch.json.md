# `.vscode/launch.json` — 실행 및 디버깅 설정

> 프로그램을 **어떻게 실행하고 디버깅할지**를 정의하는 파일.
> F5 키 하나로 복잡한 실행 환경을 재현할 수 있게 해줌.

---

## 💡 한 줄 요약

> **"F5를 눌렀을 때 무슨 일이 일어날지"를 미리 정의해두는 파일.**

---

## 🗂️ 위치와 구조

```
프로젝트 루트/
└── .vscode/
    └── launch.json   ← 여기
```

파일의 기본 뼈대:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "실행 구성 이름",
      "type": "언어/런타임",
      "request": "launch 또는 attach",
      ...
    }
  ]
}
```

### 핵심 필드 설명

| 필드 | 역할 |
|------|------|
| `version` | launch.json 스펙 버전 (현재 `"0.2.0"` 고정) |
| `configurations` | 실행 구성 목록 (여러 개 등록 가능) |
| `name` | 드롭다운에 표시될 구성 이름 |
| `type` | 사용할 디버거 종류 (`python`, `node`, `cppdbg` 등) |
| `request` | `launch`(직접 실행) 또는 `attach`(실행 중 프로세스에 연결) |

---

## 🔤 request 타입의 차이

| `launch` | `attach` |
|----------|----------|
| VS Code가 직접 프로그램을 실행 | 이미 실행 중인 프로세스에 디버거 연결 |
| 개발 중 일반적인 디버깅에 사용 | 서버·도커 컨테이너·원격 프로세스 디버깅에 사용 |
| 프로세스 제어권을 VS Code가 가짐 | 프로세스는 독립적으로 실행 중 |

---

## 📋 언어별 실전 예시

### Python — 현재 파일 실행

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Current File",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal"
    }
  ]
}
```

### Python — 특정 파일 + 인수·환경변수 전달

```json
{
  "name": "Python: main.py with args",
  "type": "python",
  "request": "launch",
  "program": "${workspaceFolder}/main.py",
  "args": ["--env", "production", "--port", "8080"],
  "env": {
    "DATABASE_URL": "sqlite:///dev.db",
    "DEBUG": "true"
  },
  "console": "integratedTerminal"
}
```

### Node.js — 서버 실행

```json
{
  "name": "Node: Launch Server",
  "type": "node",
  "request": "launch",
  "program": "${workspaceFolder}/src/server.js",
  "env": {
    "NODE_ENV": "development",
    "PORT": "3000"
  },
  "restart": true,
  "console": "integratedTerminal"
}
```

### 실행 중인 Node.js 프로세스에 attach

```json
{
  "name": "Node: Attach to Process",
  "type": "node",
  "request": "attach",
  "port": 9229,
  "restart": true,
  "localRoot": "${workspaceFolder}",
  "remoteRoot": "/app"
}
```

---

## 🔑 자주 쓰는 내장 변수

`launch.json` 안에서 경로를 동적으로 참조할 때 사용.

| 변수 | 의미 |
|------|------|
| `${file}` | 현재 에디터에 열린 파일 경로 |
| `${workspaceFolder}` | 프로젝트 루트 폴더 경로 |
| `${fileBasename}` | 현재 파일 이름 (확장자 포함) |
| `${fileBasenameNoExtension}` | 현재 파일 이름 (확장자 제외) |
| `${fileDirname}` | 현재 파일이 있는 폴더 경로 |
| `${env:변수명}` | 시스템 환경 변수 참조 |
| `${input:변수명}` | 실행 시 사용자 입력 받기 |

---

## 🔒 왜 VS Code가 보안 경고를 띄우나

`launch.json`은 3개의 `.vscode` 파일 중 **가장 직접적인 코드 실행 권한**을 가짐.

```json
{
  "name": "악성 예시",
  "type": "node",
  "request": "launch",
  "program": "${workspaceFolder}/malware.js"
}
```

F5 한 번으로 임의의 프로그램이 실행됨.
출처 불명의 프로젝트를 열었을 때 `launch.json`을 반드시 검토해야 함.

| 위험 요소 | 설명 |
|-----------|------|
| `program` 필드 | 임의의 실행 파일 지정 가능 |
| `env` 필드 | 민감한 환경변수 주입 가능 |
| `preLaunchTask` | 실행 전 자동으로 다른 명령 실행 |
| `postDebugTask` | 디버그 종료 후 자동 명령 실행 |

---

## ⚙️ 고급 활용 패턴

### 여러 구성 등록 (드롭다운 선택)

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "🐍 Python: Dev",
      "type": "python",
      "request": "launch",
      "program": "${workspaceFolder}/main.py",
      "env": { "ENV": "development" }
    },
    {
      "name": "🚀 Python: Prod (dry-run)",
      "type": "python",
      "request": "launch",
      "program": "${workspaceFolder}/main.py",
      "env": { "ENV": "production" }
    }
  ]
}
```

→ 상단 디버그 드롭다운에서 원하는 구성 선택 후 F5

### preLaunchTask 연동 (tasks.json과 함께 사용)

실행 전에 `tasks.json`의 빌드 작업을 먼저 수행.

```json
{
  "name": "C++: Build and Debug",
  "type": "cppdbg",
  "request": "launch",
  "program": "${workspaceFolder}/build/app",
  "preLaunchTask": "C++: Build"
}
```

---

## ✅ 정리 요약

```
📍 위치       →  .vscode/launch.json
🎯 역할       →  F5 실행/디버깅 구성 정의
⚡ 작동 시점   →  F5 키 또는 디버그 실행 버튼 클릭 시
🔒 보안 위험  →  임의 프로그램 실행 가능 → 출처 확인 필수
💡 핵심 필드  →  type / request / program / args / env
```

---

*작성일: 2026-03-15 | VS Code .vscode 폴더 완전 정리 시리즈*
