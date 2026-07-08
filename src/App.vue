<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

// Monday 13 July 2026, 09:00 South African Standard Time (SAST, UTC+2)
const target = new Date('2026-07-13T09:00:00+02:00')

const now = ref(new Date())
let timer

onMounted(() => {
  timer = setInterval(() => {
    now.value = new Date()
  }, 1000)
})

onUnmounted(() => {
  clearInterval(timer)
})

const remaining = computed(() => Math.max(0, target - now.value))
const finished = computed(() => remaining.value === 0)

const pad = (n) => String(n).padStart(2, '0')

const parts = computed(() => {
  const total = Math.floor(remaining.value / 1000)
  return {
    days: Math.floor(total / 86400),
    hours: pad(Math.floor((total % 86400) / 3600)),
    minutes: pad(Math.floor((total % 3600) / 60)),
    seconds: pad(total % 60),
  }
})
</script>

<template>
  <main class="countdown">
    <div v-if="!finished" class="clock">
      <div class="unit">
        <span class="value">{{ parts.days }}</span>
        <span class="label">days</span>
      </div>
      <span class="sep">:</span>
      <div class="unit">
        <span class="value">{{ parts.hours }}</span>
        <span class="label">hours</span>
      </div>
      <span class="sep">:</span>
      <div class="unit">
        <span class="value">{{ parts.minutes }}</span>
        <span class="label">minutes</span>
      </div>
      <span class="sep">:</span>
      <div class="unit">
        <span class="value">{{ parts.seconds }}</span>
        <span class="label">seconds</span>
      </div>
    </div>
    <div v-else class="done">Time's up!</div>
  </main>
</template>

<style scoped>
.countdown {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 1rem;
}

.clock {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
}

.unit {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-width: 4.5rem;
}

.value {
  font-size: clamp(2.5rem, 12vw, 6rem);
  font-weight: 700;
  line-height: 1;
  font-variant-numeric: tabular-nums;
  color: #1e293b;
}

.label {
  margin-top: 0.5rem;
  font-size: clamp(0.7rem, 2vw, 0.9rem);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: #64748b;
}

.sep {
  font-size: clamp(2rem, 10vw, 5rem);
  font-weight: 300;
  line-height: 1;
  color: #cbd5e1;
}

.done {
  font-size: clamp(2rem, 10vw, 5rem);
  font-weight: 700;
  color: #42b883;
}
</style>
