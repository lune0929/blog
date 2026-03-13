---
title: Hoon Note
---

<style>
.home-hero {
  padding: 1.5rem 0 0.5rem 0;
}

.home-badge {
  display: inline-block;
  padding: 0.35rem 0.75rem;
  border: 1px solid var(--lightgray);
  border-radius: 999px;
  font-size: 0.85rem;
  margin-bottom: 1rem;
  color: var(--secondary);
  background: color-mix(in srgb, var(--light) 70%, transparent);
}

.home-title {
  font-size: 2.3rem;
  font-weight: 800;
  line-height: 1.15;
  margin: 0 0 0.8rem 0;
}

.home-subtitle {
  font-size: 1.05rem;
  line-height: 1.8;
  color: var(--darkgray);
  margin: 0 0 1.5rem 0;
  max-width: 860px;
}

.home-actions {
  display: flex;
  gap: 0.75rem;
  flex-wrap: wrap;
  margin: 1.2rem 0 2rem 0;
}

.home-btn {
  display: inline-block;
  padding: 0.75rem 1rem;
  border-radius: 12px;
  text-decoration: none;
  font-weight: 700;
  border: 1px solid var(--lightgray);
  transition: transform 0.15s ease, opacity 0.15s ease;
}

.home-btn:hover {
  transform: translateY(-1px);
  opacity: 0.95;
}

.home-btn.primary {
  background: var(--secondary);
  color: white !important;
  border-color: var(--secondary);
}

.home-btn.secondary {
  background: transparent;
  color: var(--dark);
}

.home-section {
  margin-top: 2.5rem;
}

.home-section h2 {
  margin-bottom: 0.9rem;
}

.home-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1rem;
}

.home-card {
  border: 1px solid var(--lightgray);
  border-radius: 18px;
  padding: 1.15rem 1.1rem;
  background: color-mix(in srgb, var(--light) 60%, transparent);
}

.home-card h3 {
  margin: 0 0 0.55rem 0;
  font-size: 1.05rem;
}

.home-card p {
  margin: 0;
  color: var(--gray);
  line-height: 1.7;
  font-size: 0.96rem;
}

.home-list {
  margin-top: 0.8rem;
}

.home-list li {
  margin: 0.45rem 0;
}

.home-quote {
  margin-top: 2rem;
  padding: 1.2rem 1.1rem;
  border-left: 4px solid var(--secondary);
  background: color-mix(in srgb, var(--light) 65%, transparent);
  border-radius: 10px;
  color: var(--darkgray);
  line-height: 1.8;
}

@media (max-width: 900px) {
  .home-grid {
    grid-template-columns: 1fr;
  }

  .home-title {
    font-size: 1.8rem;
  }
}
</style>

<div class="home-hero">
  <div class="home-badge">Personal Knowledge Archive · Hoon Note</div>
  <h1 class="home-title">생각을 정리하고,<br>지식이 연결되는 개인 지식 베이스</h1>
<div class="home-actions">
    <a class="home-btn primary" href="./머리%20정리">바로 읽기</a>
    <a class="home-btn secondary" href="./데일%20카네기%20인간관계론">최근 글 보기</a>
  </div>
</div>

<div class="home-quote">
  메모는 쌓이면 저장소가 되지만,<br>
  연결되면 지식이 되고, 다시 꺼내 쓰면 자산이 됩니다.
</div>
