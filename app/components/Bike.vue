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
const height = window.innerHeight

const bikeX = ref(0)
const bikeY = ref(0)

const ease = 0.08
let animationFrame

function animate() {
  // Lerp towards the cursor
  bikeX.value += (x.value - bikeX.value) * ease
  bikeY.value += (height * 0.5 + y.value * 0.25 - bikeY.value) * ease

  animationFrame = requestAnimationFrame(animate)
}

onMounted(() => {
  bikeX.value = x.value
  bikeY.value = height * 0.5 + y.value * 0.25
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
  width: 40px;
  height: 40px;
  border-radius: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
  z-index: 9999;
}
</style>
