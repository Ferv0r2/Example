<script setup lang="ts">
defineProps<{
  msg: string
}>()
</script>

<template>
  <div class="message-box-wrapper">
    <TransitionGroup tag="span" name="typing">
      <span v-for="(word, idx) in msg" :key="word + idx">{{ word }}</span>
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
  transition: opacity 1s ease;
}
</style>
