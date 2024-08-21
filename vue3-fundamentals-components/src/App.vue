<script setup lang="ts">
import PlanPicker from '@/components/PlanPicker.vue'
import GithubCard from '@/components/GithubCard.vue'
import AppAlert from '@/components/AppAlert.vue'

import { ref } from 'vue'

const showCoffeePlan = ref(false)
const showGithubCards = ref(false)
const showAlerts = ref(true)

const show = ref(true)

const alerts = ref([
  {
    type: 'info',
    message: 'New software update available.'
  },
  {
    type: 'success',
    message: 'Your purchase has been confirmed!'
  },
  {
    type: 'warning',
    message: 'Invalid email address!'
  },
  {
    type: 'error',
    message: 'Task failed!'
  }
])
const handleClose = (message: string) => {
  alerts.value = alerts.value.filter((a) => a.message !== message)
}
</script>

<template>
  <label for=""><input type="checkbox" v-model="showCoffeePlan" />Show Coffee Plan</label>
  <label for=""><input type="checkbox" v-model="showGithubCards" />Show Github Cards</label>
  <label for=""><input type="checkbox" v-model="showAlerts" />Show Alerts</label>

  <div class="content" v-if="showCoffeePlan">
    <h1 class="title">Coffee Plans</h1>

    <h2 class="subtitle">
      We travel the world to source the very best single origin coffee for you
    </h2>

    <label for=""><input type="checkbox" v-model="show" />Show Plan Picker</label>
    <PlanPicker v-if="show" />
  </div>

  <div v-if="showGithubCards">
    <GithubCard username="lucavas" />
    <GithubCard username="danielkellyio" />
    <GithubCard username="hootlex" />
  </div>

  <div v-if="showAlerts" class="p-5 flex flex-col gap-3">
    <AppAlert
      v-for="{ type, message } in alerts"
      :key="message"
      :type="type"
      @closed="handleClose(message)"
      >{{ message }}</AppAlert
    >
    <pre>{{ alerts }}</pre>
  </div>
</template>

<style scoped></style>
