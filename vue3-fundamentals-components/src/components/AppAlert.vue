<script setup lang="ts">
import IconInfo from './icons/IconInfo.vue'
import IconSuccess from './icons/IconSuccess.vue'
import IconWarning from './icons/IconWarning.vue'
import IconError from './icons/IconError.vue'
import { computed, ref } from 'vue'

const props = defineProps({
  type: { type: String, required: true }
})
const emits = defineEmits(['closed'])

const icon = computed(() => {
  return {
    info: IconInfo,
    warning: IconWarning,
    error: IconError,
    success: IconSuccess
  }[props.type]
})

const alertType = computed(() => {
  return {
    info: 'alert-info',
    warning: 'alert-warning',
    error: 'alert-error',
    success: 'alert-success'
  }[props.type]
})

const closed = ref(false)
const close = () => {
  closed.value = true
  emits('closed')
}
</script>

<template>
  <div v-if="!closed" role="alert" :class="`alert ${alertType}`">
    <component :is="icon" />
    <span>
      <slot></slot>
    </span>
    <button @click="close">X</button>
  </div>
</template>
