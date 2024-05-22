<script setup lang="ts">
import { ref } from 'vue'
import MessageBox from '@/components/MessageBox.vue'

const firstDone = ref<boolean>(false)
const onShowMessage = () => {
  firstDone.value = true
}
</script>

<template>
  <main>
    <h1>Example</h1>
    <section class="box-container">
      <Transition name="box" appear>
        <MessageBox show msg="Hello, world!" @complete="onShowMessage" />
      </Transition>
      <Transition name="box">
        <MessageBox v-if="firstDone" msg="Welcome to the Example message." />
      </Transition>
    </section>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  width: 100%;
  gap: 16px;
}
.box-container {
  display: flex;
  flex-direction: column;
  width: 100%;
  background-color: #999;
  border-radius: 16px;
  padding: 16px;
  gap: 16px;
}
.second-box:not(.show) {
  opacity: 0;
}
.box-enter-from {
  opacity: 0;
  transform: translateY(8px);
}
.box-enter-to {
  opacity: 1;
  transform: translateY(0);
}
.box-enter-active {
  transition: all 0.5s ease;
}
</style>
