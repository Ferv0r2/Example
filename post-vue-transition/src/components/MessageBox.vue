<script setup lang="ts">
import { ref, onMounted } from 'vue'

const props = defineProps<{
  msg: string
}>()

const emits = defineEmits<{
  (event: 'complete'): void
}>()

const typingMessage = ref('')

const typeMessage = () => {
  let i = 0
  const interval = setInterval(() => {
    if (i === props.msg.length) {
      clearInterval(interval)
      emits('complete')
      return
    }
    typingMessage.value += props.msg[i]
    i++
  }, 50)
}

onMounted(() => {
  typeMessage()
})
</script>

<template>
  <div class="message-box-wrapper">
    <TransitionGroup tag="span" name="typing">
      <span v-for="(word, idx) in typingMessage" :key="word + idx">{{ word }}</span>
    </TransitionGroup>
  </div>
</template>

<style scoped>
.message-box-wrapper {
  position: relative;
  padding: 8px 16px;
  background-color: #fff;
  border-radius: 8px;
}
.message-box-wrapper::before {
  content: '';
  position: absolute;
  display: inline-block;
  top: 4px;
  left: -4px;
  width: 12px;
  height: 12px;
  transform: rotate(45deg);
  background-color: #fff;
}
span {
  color: #111;
  font-weight: 600;
}
.typing-enter-from {
  opacity: 0;
}
.typing-enter-to {
  opacity: 1;
}
.typing-enter-active {
  transition: opacity 0.01s;
}
</style>
