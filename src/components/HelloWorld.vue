<template>
  <div
    class="select-none min-h-screen bg-neutral-900 flex justify-center items-center p-8"
  >
    <div
      class="bg-neutral-800 rounded-lg border border-white shadow-md shadow-neutral-700 w-full p-12"
    >
      <div class="flex items-center gap-4">
        <h1 class="w-full text-3xl font-bold text-white">{{ header }}</h1>
        <button class="active:scale-90 duration-300" @click="toggleEditing()">
          <span title="Click to Close" v-if="editing">❌</span>
          <span title="Click to Edit" v-else>📝</span>
        </button>
      </div>
      <form
        v-if="editing"
        @submit.prevent="saveItem()"
        class="flex items-center gap-4 mt-4"
      >
        <input
          class="bg-neutral-700 text-white placeholder:text-white rounded-lg p-2 w-full outline-none"
          v-model.trim="newItem"
          type="text"
          placeholder="Add an item"
        />
        <div class="shrink-0 flex items-center gap-2">
          <input
            class="accent-neutral-700 w-4 h-4"
            v-model="newItemHighPriority"
            type="checkbox"
          />
          <label class="text-white">High Priority</label>
        </div>
        <button
          class="shrink-0 py-1 px-4 rounded bg-neutral-700 hover:bg-neutral-600 active:bg-neutral-700 duration-300 text-white"
        >
          Save Item
        </button>
      </form>
      <ul class="text-white space-y-2 mt-4">
        <li
          class="flex items-center space-x-2 border-b border-neutral-700"
          v-for="({ id, label }, index) in items"
          :key="id"
        >
          <span class="bg-neutral-700 p-1 rounded-tr-full">
            {{ index + 1 }}
          </span>
          <span>{{ label }}</span>
        </li>
      </ul>
      <p v-if="items.length === 0" class="text-white">Nothing to see here</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const header = ref("Shopping List App");
const items = ref([
  { id: 146, label: "10 party hats" },
  { id: 248, label: "2 board games" },
  { id: 389, label: "20 cups" },
]);
const newItem = ref("");
const newItemHighPriority = ref(false);
const saveItem = () => {
  if (newItem.value !== "") {
    items.value.push({ id: items.value.length + 1, label: newItem.value });
    newItem.value = "";
  }
};
const editing = ref(false);
const toggleEditing = () => {
  editing.value = !editing.value;
  newItem.value = "";
};
</script>
