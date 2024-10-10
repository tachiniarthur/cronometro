<script setup>
import { ref, onMounted } from 'vue'

const daysRemaining = ref(0)
const hoursRemaining = ref(0)
const minutesRemaining = ref(0)
const secondsRemaining = ref(0)

const calculateTimeRemaining = () => {
  const targetDate = new Date('2026-11-15T00:00:00')
  const currentDate = new Date()
  const timeDifference = targetDate - currentDate

  daysRemaining.value = Math.floor(timeDifference / (1000 * 60 * 60 * 24))
  hoursRemaining.value = Math.floor((timeDifference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
  minutesRemaining.value = Math.floor((timeDifference % (1000 * 60 * 60)) / (1000 * 60))
  secondsRemaining.value = Math.floor((timeDifference % (1000 * 60)) / 1000)
}

onMounted(() => {
  calculateTimeRemaining()
  setInterval(calculateTimeRemaining, 1000)
})
</script>

<template>
  <div class="h-screen flex flex-col items-center justify-center">
    <h1 class="text-4xl font-bold text-blue-700 mb-16">Contagem Regressiva</h1>
    <div class="text-center border-4 border-blue-700 bg-blue-100 rounded-full px-16 py-40">
      <p class="text-2xl font-bold text-black">{{ daysRemaining }} dias e {{ hoursRemaining }}:{{ minutesRemaining }}:{{ secondsRemaining }}</p>
    </div>
  </div>
</template>
