<script setup>
import { ref, nextTick, useTemplateRef, onBeforeUpdate, onMounted } from 'vue'
import FoodCard from '@/components/FoodCard.vue'
const foodsList = ref([
  { name: '寿司', icon: '🍣' },
  { name: 'ラーメン', icon: '🍜' },
  { name: 'ハンバーガー', icon: '🍔' },
  { name: 'パスタ', icon: '🍝' },
  { name: '肉', icon: '🍖' },
  { name: 'ご飯', icon: '🍚' },
  { name: 'カレー', icon: '🍛' },
  { name: 'ピザ', icon: '🍕' },
  { name: '餃子', icon: '🥟' },
  { name: '焼き鳥', icon: '🍢' },
])
const shuffleArray = (array) => {
  const cloneArray = [...array]
  const result = cloneArray.reduce((_, cur, idx) => {
    const rand = Math.floor(Math.random() * (idx + 1))
    cloneArray[idx] = cloneArray[rand]
    cloneArray[rand] = cur
    return cloneArray
  })
  return result
}
foodsList.value = shuffleArray(foodsList.value)
const pickedFoodIndex = ref(0)
const nextFoodIndex = ref(1)
const isLastFood = ref(false)
const handleClick = (e, value) => {
  pickedFoodIndex.value = value
  nextFoodIndex.value += 1
  if (nextFoodIndex.value === foodsList.value.length - 1) {
    isLastFood.value = true
  }
  console.log(pickedFoodIndex.value)
  nextTick(() => {
    console.log('nextTick in handleClick')
  })
}
const name = ref('guest')
const userInput = useTemplateRef('user-input')
onMounted(() => {
  console.log(`onMounted`)
})
onBeforeUpdate(() => {
  console.log(`onBeforeUpdated : ${userInput.value.value}`)
})
const reName = (event) => {
  console.log(`rename : ${event.target.value}`)
  name.value = event.target.value
}
</script>

<template>
  <main>
    <h1 class="title">{{ name }}さん、今日何食べる？</h1>
    <p>
      名前 :
      <input type="text" @input="reName" ref="user-input" :value="name" placeholder="name" />
    </p>
    <div class="todays-food" v-if="isLastFood">
      <p>今日のご飯は、</p>
      <FoodCard :name="foodsList[pickedFoodIndex].name" :icon="foodsList[pickedFoodIndex].icon" />
      <p>に決定！</p>
    </div>
    <div class="food-card" v-else>
      <FoodCard
        @click="handleClick($event, pickedFoodIndex)"
        :name="foodsList[pickedFoodIndex].name"
        :icon="foodsList[pickedFoodIndex].icon"
      />
      <p>VS</p>
      <FoodCard
        @click="handleClick($event, nextFoodIndex)"
        :name="foodsList[nextFoodIndex].name"
        :icon="foodsList[nextFoodIndex].icon"
      />
    </div>
  </main>
</template>

<style scoped>
main {
  width: 1080px;
  margin: 0 auto;
  padding: 30px 0;
  text-align: center;
  background-color: #f0f0f0;
}
h1.title {
  font-size: 3rem;
}
.todays-food {
  font-size: 2rem;
}
</style>
