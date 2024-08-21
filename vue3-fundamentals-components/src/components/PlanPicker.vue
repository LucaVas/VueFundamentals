<script setup lang="ts">
import CoffeePlan from '@/components/CoffeePlan.vue'
import { ref, onMounted, onUnmounted } from 'vue'

const plans = ref(['The Single', 'The Curious', 'The Addict'])

const selectedCoffeePlan = ref()
const handleSelectCoffeePlan = (name: string) => (selectedCoffeePlan.value = name)

const counter = ref(0)

const plansWrapper = ref()
onMounted(() => {
  console.log(plansWrapper.value)
  setInterval(() => {
    counter.value++
    console.log(counter.value)
  }, 1000)
})
onUnmounted(() => {
  clearInterval(counter.value)
  alert('Bye bye plan picker')
})
</script>

<template>
  <div ref="plansWrapper" class="plans">
    {{ selectedCoffeePlan }}
    {{ counter }}
    <CoffeePlan
      v-for="plan in plans"
      :key="plan"
      :name="plan"
      @selected="handleSelectCoffeePlan"
      :selected="plan === selectedCoffeePlan"
    >
      <template #slot-content="{ hover }"> <em>{{ hover ? 'Hovered' : 'Not Hovered' }}</em></template>
    </CoffeePlan>
  </div>
</template>
