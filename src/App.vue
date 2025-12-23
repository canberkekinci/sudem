<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const startDate = new Date("2025-11-28T00:58:00");

const startDateText = "28 Kasım 2025";

const time = ref({
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0,
});

let interval = null;

const updateTimer = () => {
  const now = new Date();
  let diff = now - startDate;

  const days = Math.floor(diff / (1000 * 60 * 60 * 24));
  diff %= 1000 * 60 * 60 * 24;

  const hours = Math.floor(diff / (1000 * 60 * 60));
  diff %= 1000 * 60 * 60;

  const minutes = Math.floor(diff / (1000 * 60));
  diff %= 1000 * 60;

  const seconds = Math.floor(diff / 1000);

  time.value = { days, hours, minutes, seconds };
};

onMounted(() => {
  updateTimer();
  interval = setInterval(updateTimer, 1000);
});

onUnmounted(() => {
  clearInterval(interval);
});
</script>

<template>
  <div class="container">
    <h1>Sudemle Birlikte Geçen Zaman</h1>

    <div class="timer">
      <div class="box">
        <span>{{ time.days }}</span>
        <small>Gün</small>
      </div>
      <div class="box">
        <span>{{ time.hours }}</span>
        <small>Saat</small>
      </div>
      <div class="box">
        <span>{{ time.minutes }}</span>
        <small>Dakika</small>
      </div>
      <div class="box">
        <span>{{ time.seconds }}</span>
        <small>Saniye</small>
      </div>
    </div>

    <p class="note">{{ startDateText }} gününden beri 💖</p>
    <a class="link" href="https://www.youtube.com/watch?v=8ScAnaU0FFE" target="_blank">💗</a>
  </div>
  <p class="signature">canberk tarafından 💞 ile yapıldı</p>
</template>

<style scoped>
.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: #fff5f7;
  font-family: "Playfair Display", serif;
}

h1 {
  margin-bottom: 24px;
}

.timer {
  display: flex;
  gap: 20px;
}

.box {
  background: white;
  padding: 20px;
  border-radius: 16px;
  text-align: center;
  width: 90px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.box span {
  font-size: 32px;
  font-weight: bold;
}

.note {
  margin-top: 24px;
  font-style: italic;
}

.signature {
  position: fixed;
  bottom: 16px;
  right: 20px;
  font-size: 12px;
  font-style: italic;
  font-family: monospace;
}

.link {
  margin-top: 20px;
  display: inline-flex;
  align-items: center;
  justify-content: center;

  width: 48px;
  height: 48px;
  border-radius: 50%;

  background: #f6c1cc;
  color: #5a2a33;

  font-size: 22px;
  text-decoration: none;

  box-shadow: 0 6px 18px rgba(0, 0, 0, 0.08);

  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.link:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 24px rgba(0, 0, 0, 0.12);
}

@media (max-width: 600px) {
  .container {
    padding: 24px 16px;
    justify-content: center;
  }

  h1 {
    font-size: 22px;
    margin-bottom: 16px;
  }

  .timer {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 16px;
  }

  .box {
    width: 80px;
    padding: 16px;
  }

  .box span {
    font-size: 26px;
  }

  .note {
    font-size: 13px;
    margin-top: 16px;
  }

  .link {
    width: 44px;
    height: 44px;
    font-size: 20px;
    margin-top: 18px;
  }

  .signature {
    font-size: 10px;
  }
}
</style>
