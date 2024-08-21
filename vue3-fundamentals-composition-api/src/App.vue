<script setup lang="ts">
import { ref, computed } from 'vue';

type Item = {
  id: number;
  label: string;
  purchased: boolean;
  highPriority: boolean;
};

const header = ref('Shopping List App');
const items = ref<Item[]>([
  { id: 0, label: '10 party hats', purchased: true, highPriority: false },
  { id: 1, label: '2 board games', purchased: true, highPriority: false },
  { id: 2, label: '20 cups', purchased: false, highPriority: true },
]);
const newItem = ref('');
const editing = ref(false);
const newItemHighPriority = ref(false);
const characterCount = computed(() => newItem.value.length);
const reversedItems = computed(() => [...items.value].reverse()); // reverse() modifies object

const saveItem = () => {
  items.value.push({
    id: items.value.length + 1,
    label: newItem.value,
    purchased: false,
    highPriority: newItemHighPriority.value,
  });
  newItem.value = '';
  newItemHighPriority.value = false;
};
const doEdit = (e: boolean) => {
  editing.value = e;
  newItem.value = '';
  newItemHighPriority.value = false;
};
const togglePurchase = (item: Item) => {
  item.purchased = !item.purchased;
};
</script>

<template>
  <div>
    <h1>{{ header }}</h1>
    <button v-if="editing" @click="doEdit(false)">Cancel</button>
    <button v-else @click="doEdit(true)">Add</button>
  </div>

  <div class="main">
    <form v-if="editing" action="" @submit.prevent="saveItem">
      <input
        maxlength="200"
        type="text"
        placeholder="Add an item"
        v-model.trim="newItem"
      />
      <p>{{ characterCount }}/200</p>

      <label
        ><input type="checkbox" v-model="newItemHighPriority" /> High Priority
      </label>
      <div>
        <button class="btn btn-primary" :disabled="!newItem">Save Item</button>
      </div>
    </form>

    <div>
      <p v-if="!items.length">Nothing to see here</p>
      <ul v-else>
        <li
          @click="togglePurchase(item)"
          v-for="(item, index) in reversedItems"
          :key="item.id"
          :class="[
            { strikeout: item.purchased },
            { priority: item.highPriority },
          ]"
        >
          {{ item.label }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.main {
  flex-direction: column;
}

.strikeout {
  text-decoration: line-through;
}

.priority {
  color: orange;
}
</style>
