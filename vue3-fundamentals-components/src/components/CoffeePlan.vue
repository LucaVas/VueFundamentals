<script setup lang="ts">
import { ref } from 'vue'

const selected = ref(false)
const hover = ref(false)

const selectPlan = () => {
  selected.value = !selected.value
  emit('selected', props.name)
}

const props = defineProps({
  name: {
    type: String,
    default: 'Default Plan',
    required: true,
    validator(value: string) {
      return value.startsWith('The')
    },
    selected: { type: Boolean }
  }
})
const emit = defineEmits({
  eventNotValidated: null,
  selected(payload) {
    return typeof payload === 'string'
  }
})
</script>

<template>
  <div
    class="plan"
    :class="[{ 'active-plan': selected }]"
    @click="selectPlan"
    @mouseenter="hover = true"
    @mouseleave="hover = false"
  >
    <div class="description">
      <span class="title">
        {{ name }} - <slot name="slot-content" :hover="hover"> Default Slot Content </slot>
      </span>
    </div>
  </div>
</template>
