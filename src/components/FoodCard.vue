<script setup>
import {
  onMounted,
  onBeforeMount,
  onUnmounted,
  onBeforeUnmount,
  onUpdated,
  onBeforeUpdate,
} from 'vue'
defineProps({
  name: {
    type: String,
    required: true,
  },
  icon: {
    type: String,
    required: true,
  },
})
onMounted(() => {
  console.log('mounted2')
})
onUnmounted(() => {
  console.log('unmounted2')
})
onUpdated(() => {
  console.log('updated2')
})
onBeforeMount(() => {
  console.log('before mount2')
})
onBeforeUpdate(() => {
  console.log('before update2')
})
onBeforeUnmount(() => {
  console.log('before unmount2')
})
</script>
<template>
  <div class="card">
    <p class="food-name">{{ name }}</p>
    <p class="food-icon">{{ icon }}</p>
  </div>
</template>
<style scoped>
.card {
  padding: 16px;
  width: 250px;
  height: auto;
  margin: 0 auto;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #fff;
  box-shadow: 2px 2px 6px rgba(0, 0, 0, 0.4);
  font-size: 2rem;
  cursor: pointer;
}
.card:hover {
  background-color: rgb(79, 153, 228);
}
.food-icon {
  margin-top: -20px;
  font-size: 48px;
}
</style>
