<script setup lang="ts">
import { ref } from 'vue';

// 표시될 덕담 메시지를 저장할 반응형 변수
const wishMessage = ref('');
const messageVisible = ref(false);

// 덕담 목록
const wishes: string[] = [
  '보름달처럼 풍성한 행복이 가득하시길 바랍니다.',
  '가족들과 함께 웃음꽃 넘치는 즐거운 연휴 보내세요.',
  '높고 푸른 가을 하늘처럼 모든 일이 잘 풀리시기를 기원합니다.',
  '맛있는 음식 많이 드시고, 몸도 마음도 넉넉한 한가위 되세요.',
  '언제나 건강하고, 소망하는 모든 일이 이루어지길 바랍니다.'
];

// 복주머니를 클릭했을 때 실행될 함수
function revealWish() {
  const randomIndex = Math.floor(Math.random() * wishes.length);
  wishMessage.value = wishes[randomIndex];
  messageVisible.value = true;
}
</script>

<template>
  <div id="chuseok-app">
    <header class="app-header">
      <h1 class="title">풍요로운 한가위 보내세요</h1>
      <p class="subtitle">소원을 빌어보세요</p>
    </header>

    <main class="app-main">
      <!-- 보름달 SVG -->
      <svg class="full-moon" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
        <defs>
          <radialGradient id="moonGradient" cx="40%" cy="40%" r="60%">
            <stop offset="0%" style="stop-color: #ffffe0; stop-opacity: 1" />
            <stop offset="100%" style="stop-color: #f7d794; stop-opacity: 1" />
          </radialGradient>
          <filter id="moonGlow" x="-50%" y="-50%" width="200%" height="200%">
            <feGaussianBlur stdDeviation="10" result="coloredBlur" />
            <feMerge>
              <feMergeNode in="coloredBlur" />
              <feMergeNode in="SourceGraphic" />
            </feMerge>
          </filter>
        </defs>
        <circle cx="100" cy="100" r="90" fill="url(#moonGradient)" filter="url(#moonGlow)" />
        <text x="100" y="105" text-anchor="middle" fill="#594518" font-size="18" font-family="'Gowun Dodum', sans-serif">한가위</text>
      </svg>

      <!-- 덕담 섹션 -->
      <section class="wish-section">
        <div class="wish-container">
          <transition name="fade">
            <p v-if="messageVisible" class="wish-message">{{ wishMessage }}</p>
          </transition>
        </div>
        <button @click="revealWish" class="lucky-pouch-btn" aria-label="덕담 보기">
          <!-- 복주머니 SVG 아이콘 -->
          <svg class="pouch-icon" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
            <path d="M10 30 C 10 10, 90 10, 90 30 C 100 50, 100 80, 80 95 L 20 95 C 0 80, 0 50, 10 30 Z" fill="#e74c3c"/>
            <path d="M10 30 C 10 20, 90 20, 90 30 L 80 30 C 80 25, 20 25, 20 30 Z" fill="#f1c40f"/>
            <circle cx="50" cy="65" r="12" fill="#f1c40f" stroke="#c0392b" stroke-width="2"/>
            <text x="50" y="70" text-anchor="middle" font-size="15" fill="#c0392b" font-weight="bold">복</text>
          </svg>
          <span>복주머니 열기</span>
        </button>
      </section>
    </main>

    <footer class="app-footer">
      <p>© 2025 Happy Chuseok</p>
    </footer>
  </div>
</template>

<style scoped>
/* 구글 웹폰트 임포트 */
@import url('https://fonts.googleapis.com/css2?family=Gowun+Dodum&display=swap');

#chuseok-app {
  font-family: 'Gowun Dodum', sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  min-height: 100vh;
  background: linear-gradient(to bottom, #0c1445, #301934, #542d3d);
  color: white;
  text-align: center;
  padding: 2rem;
  box-sizing: border-box;
  overflow-x: hidden;
}

.app-header .title {
  font-size: 2.5rem;
  font-weight: bold;
  color: #f7d794;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
  margin: 0;
}

.app-header .subtitle {
  font-size: 1.2rem;
  color: #dfe6e9;
  opacity: 0.9;
  margin-top: 0.5rem;
}

.app-main {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
  width: 100%;
  max-width: 500px;
}

.full-moon {
  width: 200px;
  height: 200px;
  animation: gentle-rise 5s ease-in-out;
}

.wish-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.5rem;
  width: 100%;
}

.wish-container {
  min-height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.wish-message {
  font-size: 1.1rem;
  background-color: rgba(255, 255, 255, 0.1);
  padding: 1rem;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  width: 100%;
}

.lucky-pouch-btn {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem 1.5rem;
  font-family: 'Gowun Dodum', sans-serif;
  font-size: 1.1rem;
  font-weight: bold;
  color: #594518;
  background: linear-gradient(145deg, #f9e79f, #f7d794);
  border: none;
  border-radius: 50px;
  cursor: pointer;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
  transition: all 0.3s ease;
}

.lucky-pouch-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 20px rgba(247, 215, 148, 0.4);
}

.lucky-pouch-btn:active {
  transform: translateY(0);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

.pouch-icon {
  width: 30px;
  height: 30px;
}

.app-footer {
  font-size: 0.9rem;
  color: #b2bec3;
  opacity: 0.7;
}

/* 애니메이션 */
@keyframes gentle-rise {
  from {
    opacity: 0;
    transform: translateY(50px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.8s ease;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

/* 모바일 반응형 */
@media (max-width: 600px) {
  #chuseok-app {
    padding: 1rem;
  }
  .app-header .title {
    font-size: 2rem;
  }
  .app-header .subtitle {
    font-size: 1rem;
  }
  .full-moon {
    width: 150px;
    height: 150px;
  }
  .wish-message {
    font-size: 1rem;
  }
  .lucky-pouch-btn {
    padding: 0.8rem 1.2rem;
    font-size: 1rem;
  }
}
</style>
