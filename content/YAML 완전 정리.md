# YAML 완전 정리

> **YAML**은 사람이 읽기 쉬운 데이터 직렬화 언어.
> Obsidian에서는 노트 최상단의 **Front Matter** 영역에 사용되며, 태그·날짜·상태 등 메타데이터를 관리.

---

## 💡 YAML이란?

**YAML Ain't Markup Language** 의 재귀적 약자.

JSON이나 XML처럼 데이터를 구조화하는 언어지만, 훨씬 읽기 쉬운 문법이 특징.
설정 파일, 메타데이터, CI/CD 파이프라인 등 다양한 곳에서 활용.

```yaml
# JSON과 비교
# JSON 방식
{ "title": "YAML 정리", "tags": ["obsidian", "yaml"] }

# YAML 방식 (훨씬 읽기 쉬움)
title: YAML 정리
tags:
  - obsidian
  - yaml
```

---

## 📌 Obsidian에서의 YAML — Front Matter

Obsidian 노트 **맨 위**에 `---` 로 감싸면 메타데이터 영역(Front Matter)으로 인식.

```yaml
---
title: YAML 완전 정리
date: 2026-03-15
tags:
  - obsidian
  - yaml
  - 학습
status: 작성중
---

여기서부터 본문 내용...
```

> **Tip:** Front Matter는 노트 검색, 필터링, Dataview 플러그인 쿼리에 핵심적으로 활용.

---

## 🔤 기본 문법

### 키-값 쌍 (Key-Value)

가장 기본적인 형태. `키: 값` 구조.

```yaml
title: 나의 첫 번째 노트
author: 홍길동
date: 2026-03-15
published: true
rating: 5
```

> **주의:** 콜론(`:`) 뒤에 반드시 **공백** 하나 필요.

---

### 문자열 (String)

```yaml
# 따옴표 없이도 사용 가능
title: Obsidian 활용 가이드

# 공백이나 특수문자 포함 시 따옴표 사용
subtitle: "Obsidian: 최고의 노트 앱"

# 여러 줄 문자열 — | 사용 (줄바꿈 유지)
description: |
  Obsidian은 마크다운 기반의
  지식 관리 도구.
  로컬 파일로 데이터를 저장.

# 여러 줄 문자열 — > 사용 (줄바꿈을 공백으로 합침)
summary: >
  Obsidian은 마크다운 기반의
  지식 관리 도구.
```

---

### 숫자 / 불리언 / Null

```yaml
# 숫자
page_count: 42
version: 1.5

# 불리언 (참/거짓)
published: true
draft: false

# Null (값 없음)
due_date: null
due_date:        # 값을 비워도 null로 처리
```

---

### 리스트 (List)

```yaml
# 블록 스타일 (가독성 좋음)
tags:
  - obsidian
  - markdown
  - 생산성

# 인라인 스타일
tags: [obsidian, markdown, 생산성]

# 숫자 리스트
scores:
  - 90
  - 85
  - 92
```

---

### 중첩 구조 (Nested)

들여쓰기(스페이스 2칸)로 계층 구조 표현. **탭(Tab) 사용 불가**.

```yaml
author:
  name: 홍길동
  email: hong@example.com
  social:
    github: honggildong
    twitter: "@hong"

project:
  name: 나의 Obsidian 볼트
  version: 2.0
  settings:
    theme: dark
    font_size: 16
```

---

### 주석 (Comment)

`#` 기호로 주석 작성. 해당 줄은 데이터로 처리되지 않음.

```yaml
# 이 파일은 프로젝트 설정
title: 내 프로젝트  # 프로젝트 이름
version: 1.0       # 현재 버전
# draft: true      # 임시로 비활성화
```

---

## 📋 데이터 타입 요약

| 타입 | 예시 | 설명 |
|------|------|------|
| 문자열 | `title: 제목` | 기본 텍스트 |
| 숫자 | `count: 42` | 정수 / 실수 |
| 불리언 | `done: true` | true / false |
| Null | `value: null` | 빈 값 |
| 리스트 | `- item` | 순서 있는 목록 |
| 맵(객체) | `key: value` | 키-값 쌍의 집합 |

---

## 🗂️ Obsidian Front Matter 실전 예시

### 일반 노트

```yaml
---
title: Docker 기초 정리
date: 2026-03-15
tags:
  - 개발
  - docker
  - 학습
status: 완료
source: https://docs.docker.com
---
```

### 프로젝트 관리

```yaml
---
title: 웹사이트 리뉴얼 프로젝트
created: 2026-01-01
deadline: 2026-06-30
priority: 높음
assignee: 홍길동
progress: 45
tags:
  - 프로젝트
  - 진행중
---
```

### 독서 기록

```yaml
---
title: "Clean Code"
author: Robert C. Martin
started: 2026-02-10
finished: 2026-03-01
rating: 5
genre:
  - 개발
  - 클린코드
review: 강력 추천
---
```

---

## ⚠️ 자주 하는 실수

```yaml
# ❌ 잘못된 예시
title:제목          # 콜론 뒤 공백 없음
  title: 제목       # 불필요한 들여쓰기
tags: [a, b, c      # 닫는 괄호 누락

# ✅ 올바른 예시
title: 제목
tags: [a, b, c]
```

| 실수 | 원인 | 해결 |
|------|------|------|
| 콜론 뒤 공백 없음 | `title:제목` | `title: 제목` |
| Tab으로 들여쓰기 | 탭 키 사용 | 스페이스 2칸 사용 |
| 따옴표 미사용 | 특수문자 포함 값 | `"값: 특수문자"` |
| `---` 누락 | Front Matter 미인식 | 노트 맨 위에 `---` 추가 |

---

## ✅ 정리 요약

```
📌 Front Matter  →  노트 상단 --- 안에 메타데이터 작성
🔤 기본 구조     →  키: 값  (콜론 뒤 공백 필수)
📋 리스트        →  - 항목  또는  [항목1, 항목2]
🏗️ 중첩 구조    →  들여쓰기 2칸 (Tab 금지)
💬 주석          →  # 기호 사용
```

> **Tip:** Obsidian의 **Dataview** 플러그인을 쓰면 Front Matter 데이터를 기반으로 노트를 표/리스트로 자동 조회 가능.


| 항목     | HTML(HyperText Markup Language) | XML(eXtensible Markup Language) | JSON(JavaScript Object Notation)                                               | YAML(YAML Ain't Markup Language: 야믈)                                                                                                             |
| ------ | ------------------------------- | ------------------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| 주용도    | 웹 문서 표시                         | 구조화 데이터 표현                      | 데이터 교환                                                                         | 설정/데이터 표현                                                                                                                                        |
| 읽는 주체  | 브라우저                            | 시스템/프로그램                        | 프로그램                                                                           | 사람 + 프로그램                                                                                                                                        |
| 문법 방식  | 태그                              | 태그                              | 중괄호, 대괄호                                                                       | 들여쓰기                                                                                                                                             |
| 가독성    | 화면 구조 중심                        | 장황한 편                           | 비교적 단순                                                                         | 가장 읽기 쉬운 편                                                                                                                                       |
| 엄격성    | 중간                              | 높음                              | 높음                                                                             | 들여쓰기 실수에 민감                                                                                                                                      |
| 대표 사용처 | 웹페이지                            | 일부 기업 시스템, 설정, 데이터 교환           | REST API(Representational State Transfer Application Programming Interface) 응답 | Docker Compose(Docker Compose: 도커 다중 컨테이너 구성 도구), </br>GitHub Actions(GitHub Actions: 깃허브 자동화 기능), </br>Kubernetes(Kubernetes: 컨테이너 오케스트레이션 플랫폼) |
**HTML**
```html
<div class="user">  
  <span class="name">민수</span>  
  <span class="age">20</span>  
</div>
```
**XML**
```xml
<user>  
  <name>민수</name>  
  <age>20</age>  
</user>
```
**JSON**
```json
{  
  "name": "민수",  
  "age": 20  
}
```
**YAML**
```yaml
name: 민수  
age: 20
```
---

*작성일: 2026-03-15 | Obsidian 노트 작성 팁 시리즈*
