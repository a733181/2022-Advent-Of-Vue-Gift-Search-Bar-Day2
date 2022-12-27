<template>
  <div class="container mx-auto flex justify-center items-center h-full">
    <div class="flex items-center flex-col">
      <p class="py-2 px-3 mb-5 bg-slate-500 text-white rounded-lg self-start">{{ data.setup }}</p>
      <p v-if="type !== 0" class="mb-5 bg-orange-600 text-white py-2 px-3 rounded-lg self-end">{{ data.delivery }}</p>
      <button type="button" class="w-44 bg-green text-white rounded-lg py-2" @click="clickHandler">
        {{ type === 1 ? 'Another' : 'Tell Me!' }}
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
const type = ref(0)
const data = ref({})
const clickHandler = () => {
  if (type.value === 1) {
    getHandler()
    type.value = 0
  } else {
    type.value = 1
  }
}
const getHandler = async () => {
  try {
    const result = await fetch('https://v2.jokeapi.dev/joke/christmas')
    data.value = await result.json()
  } catch (err) {}
}
onMounted(() => {
  type.value = 0
  getHandler()
})
</script>
