<script setup lang="ts">
import { ref, onMounted } from 'vue'

const props = defineProps({
  username: { type: String, required: true }
})

const user = ref()

const fetchUserData = async (username: string) => {
  const res = await fetch(`https://api.github.com/users/${username}`)
  const data = await res.json()
  user.value = data
}

onMounted(async () => {
  await fetchUserData(props.username)
})
</script>

<template>
  <!-- <pre>{{ user }}</pre> -->
  <div v-if="user" class="card card-side bg-base-100 shadow-xl m-5">
    <figure>
      <img
        :src="user.avatar_url"
        alt="Avatar"
      />
    </figure>
    <div class="card-body">
      <h2 class="card-title">{{ user.name }}</h2>
      <p>
        <strong>Followers: </strong> {{ user.followers }}
        <strong>Following: </strong> {{ user.following }}
      </p>
      <div class="card-actions justify-end">
        <a :href="user.html_url" class="btn btn-primary">View Profile</a>
      </div>
    </div>
  </div>
</template>
