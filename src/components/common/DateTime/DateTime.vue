<template>
  <div>
    {{ date }}
  </div>
</template>

<script setup>
import { onActivated, onDeactivated, onMounted, ref } from 'vue';
import dayjs from 'dayjs';
import { onUnmounted } from 'vue';

const props = defineProps({
  format: {
    type: String,
    default: 'YYYY-MM-DD HH:mm:ss'
  }
})

const date = ref(dayjs().format(props.format))
let timer = null

function createDateTimer() {
  timer = setInterval(() => {
    date.value = dayjs().format(props.format)
  }, 1000)
}

function clearDateTimer() {
  if (timer) {
    clearInterval(timer)
    timer = null
  }
}

onMounted(() => {
  createDateTimer()
})

onUnmounted(() => {
  clearDateTimer()
})

onActivated(() => {
  createDateTimer()
})

onDeactivated(() => {
  clearDateTimer()
})

</script>

<style lang="scss" scoped></style>