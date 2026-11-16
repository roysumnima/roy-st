<!-- <template>
  <UButton>🚲</UButton>
</template> -->


<!-- <script setup>
import { useMouse } from '@vueuse/core'

const { x } = useMouse()
</script>

<template>
  <div class="follower" :style="{ left: `${x}px` }" />
</template>

<style scoped>
.follower {
  position: fixed;
  top: 50%;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: #6366f1;
  transform: translate(-50%, -50%);
  pointer-events: none;
  z-index: 9999;
  transition: left 0.08s linear;
}
</style> -->


<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { useMouse } from '@vueuse/core'

const { x, y } = useMouse()

const bikeX = ref(0)
const bikeY = ref(0)

const streetWidth = 0.6
let horizon = 0 // value updated onMounted to be 60% of the window height
const ease = 0.08
let animationFrame

function animate() {
  // Lerp towards the cursor
  bikeX.value += (x.value - bikeX.value - 20) * ease

  calculateBikeY()

  animationFrame = requestAnimationFrame(animate)
}

function calculateBikeY() {
  const targetY = y.value < horizon
    ? horizon + (horizon - y.value) * streetWidth
    : horizon + (y.value - horizon) * 1

  bikeY.value += (targetY - bikeY.value -50 ) * ease
}

onMounted(() => {
  horizon = 0.6 * window.innerHeight
  bikeX.value = x.value
  bikeY.value = y.value
  animate()
})

onUnmounted(() => {
  cancelAnimationFrame(animationFrame)
})
</script>

<template>
  <div
    class="bike"
    :style="{
      left: `${bikeX}px`,
      top: `${bikeY}px`,
      }"
      >
      🚲
      </div>
</template>

<style scoped>
.bike {
  position: fixed;
  top: 50%;
  width: 100px;
  height: 100px;
  font-size: 4rem;
  border-radius: 50%;
  /* transform: translate(-50%, -50%); */
  pointer-events: none;
  z-index: 9999;
}
</style>
