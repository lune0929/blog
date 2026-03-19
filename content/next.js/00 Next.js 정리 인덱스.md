# Next.js 정리 인덱스

> [!note] 목표  
Next.js를 개념 → 구조 → 동작 원리 → 실전 패턴 순서로 정리하려고 만든 문서임.

## 전체 구조  
  
- [[01. Next.js란 무엇인가]]  
- [[02. 개발 환경과 프로젝트 시작]]  
- [[03. 폴더 구조와 기본 흐름]]  
- [[04. 라우팅 구조]]  
- [[05. 레이아웃과 페이지 구성]]  
- [[06. 렌더링 방식]]  
- [[07. 서버 컴포넌트와 클라이언트 컴포넌트]]  
- [[08. 데이터 가져오기]]  
- [[09. 서버 액션과 폼 처리]]  
- [[10. API(Route Handler-서버 요청 처리 경로)]]  
- [[11. 스타일링]]  
- [[12. 이미지, 폰트, 정적 파일]]  
- [[13. 상태 관리]]  
- [[14. 인증과 인가]]  
- [[15. 성능 최적화]]  
- [[16. 에러 처리와 로딩 처리]]  
- [[17. 환경 변수와 설정]]  
- [[18. 배포와 운영]]  
- [[19. 실전 아키텍처 패턴]]  
- [[20. 면접/실무 체크포인트]]

### 내가 헷갈리는 것  
- 서버 컴포넌트(Server Component: 서버에서 실행되는 컴포넌트)와 
      클라이언트 컴포넌트(Client Component: 브라우저에서 실행되는 컴포넌트) 차이  
- 렌더링 방식 차이  
- App Router(App Router: 앱 디렉터리 기반 라우팅 방식) 구조  
- 데이터 가져오는 위치  
- 캐시(Cache: 재사용을 위해 저장해 둔 데이터) 동작 방식  
  
### 꼭 비교할 것  
- Next.js vs React(React: 사용자 인터페이스 구축용 라이브러리)  
- Pages Router(Pages Router: pages 디렉터리 기반 라우팅 방식) vs 
      App Router(App Router: app 디렉터리 기반 라우팅 방식)  
- SSR(Server-Side Rendering: 서버 측 렌더링) vs 
      CSR(Client-Side Rendering: 클라이언트 측 렌더링) vs 
      SSG(Static Site Generation: 정적 사이트 생성) vs 
      ISR(Incremental Static Regeneration: 점진적 정적 재생성)
