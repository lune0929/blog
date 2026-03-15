# Obsidian 코드블록 언어 완전 정리

> Obsidian에서 코드블록을 작성할 때 ` ``` ` 뒤에 언어명을 붙이면 **문법 강조(Syntax Highlighting)** 가 적용.
> 자주 쓰이는 언어 키워드를 카테고리별로 정리.

---

## 💡 기본 사용법

코드블록은 백틱(`` ` ``) 세 개로 감싸고, 첫 줄에 언어 키워드를 명시.

````markdown
```python
print("Hello, Obsidian!")
```
````

---

## 📋 카테고리별 언어 목록

### 📝 일반 텍스트

서식 없이 순수 텍스트를 표시할 때 사용. 언어명을 생략해도 동일하게 작동.

| 키워드 | 설명 |
|--------|------|
| `text` | 일반 텍스트 |
| `txt` | 일반 텍스트 (축약형) |
| *(생략)* | 언어명 없이 사용 가능 |

---

### 🖥️ 쉘 / 터미널

커맨드라인 명령어나 스크립트를 표시할 때 사용.

| 키워드 | 설명 |
|--------|------|
| `sh` | 일반 쉘 스크립트 |
| `bash` | Bash 스크립트 |
| `shell` | 쉘 (범용) |
| `zsh` | Zsh 스크립트 |
| `powershell` | PowerShell |
| `ps1` | PowerShell (축약형) |
| `cmd` | Windows 명령 프롬프트 |
| `batch` | Windows 배치 파일 |

**예시:**
```bash
#!/bin/bash
echo "Obsidian 노트 자동 백업 시작"
cp -r ~/vault ~/backup/vault_$(date +%Y%m%d)
```

---

### 🌐 웹 프론트엔드

HTML, CSS, JavaScript 등 웹 관련 언어.

| 키워드 | 설명 |
|--------|------|
| `html` | HTML |
| `css` | CSS |
| `scss` | SCSS (CSS 전처리기) |
| `sass` | Sass |
| `javascript` / `js` | JavaScript |
| `typescript` / `ts` | TypeScript |
| `json` | JSON 데이터 형식 |
| `xml` | XML |
| `yaml` / `yml` | YAML 설정 파일 |
| `toml` | TOML 설정 파일 |

**예시:**
```json
{
  "name": "my-obsidian-plugin",
  "version": "1.0.0",
  "description": "나만의 Obsidian 플러그인"
}
```

---

### 💻 프로그래밍 언어

범용 프로그래밍 언어 목록.

| 키워드 | 설명 |
|--------|------|
| `python` / `py` | Python |
| `java` | Java |
| `c` | C |
| `cpp` | C++ |
| `csharp` / `cs` | C# |
| `go` | Go |
| `rust` | Rust |
| `kotlin` | Kotlin |
| `swift` | Swift |
| `php` | PHP |
| `ruby` | Ruby |
| `r` | R (통계 언어) |
| `sql` | SQL |

**예시:**
```python
# Obsidian 노트 제목 목록 출력
import os

vault_path = "./my_vault"
for file in os.listdir(vault_path):
    if file.endswith(".md"):
        print(f"📝 {file}")
```

---

### ⚙️ 설정 / 문서

프로젝트 설정 파일이나 문서 형식.

| 키워드 | 설명 |
|--------|------|
| `markdown` / `md` | Markdown |
| `ini` | INI 설정 파일 |
| `dockerfile` | Dockerfile |
| `nginx` | Nginx 설정 |
| `gitignore` | .gitignore 파일 |
| `properties` | Java Properties 파일 |

**예시:**
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
CMD ["node", "server.js"]
```

---

### 🗂️ 데이터 / 기타

데이터 처리 및 특수 목적 언어.

| 키워드 | 설명 |
|--------|------|
| `csv` | CSV 데이터 |
| `diff` | 파일 변경 비교 (Git diff 등) |
| `regex` | 정규표현식 |
| `latex` / `tex` | LaTeX 수식/문서 |
| `graphql` | GraphQL 쿼리 |

**예시:**
```diff
- 기존 노트 제목: 코드박스 종류
+ 수정된 노트 제목: Obsidian 코드블록 언어 완전 정리
```

---

## ✅ 정리 요약

```
📝 텍스트    → text, txt
🖥️ 터미널   → bash, shell, powershell, cmd
🌐 웹       → html, css, js, ts, json, yaml
💻 프로그래밍 → python, java, c, cpp, go, rust, sql ...
⚙️ 설정     → dockerfile, nginx, ini, markdown
🗂️ 기타     → diff, regex, latex, graphql
```

> **Tip:** 언어 키워드는 대소문자 구분 없음. 소문자로 쓰는 것이 관례.

---

*작성일: 2026-03-15 | Obsidian 노트 작성 팁 시리즈*
