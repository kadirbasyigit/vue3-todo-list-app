<script setup lang="ts">
import { ref } from 'vue';
import { PlusCircleIcon } from '@heroicons/vue/24/outline';
import { TrashIcon } from '@heroicons/vue/24/solid';

const newTodo = ref('');
const todos = ref<string[]>([]);
const addTodo = () => {
  if (newTodo.value.trim() === '') return;
  todos.value.push(newTodo.value);
  newTodo.value = '';
};
</script>

<template>
  <div
    class="absolute inset-0 -z-10 h-full w-full bg-white bg-[radial-gradient(#e5e7eb_1px,transparent_1px)] [background-size:16px_16px]"
  ></div>
  <div
    class="min-h-screen flex items-center justify-center font-[Montserrat] font-medium"
  >
    <div class="bg-blue-100 w-2/6 p-8 rounded-lg shadow-lg">
      <h2 class="text-3xl text-blue-500 text-center">Yapılacaklar Listesi</h2>
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        type="text"
        class="w-full mt-4 p-2 border border-gray-300 rounded-lg"
        placeholder="Yapılacak şeyi yazın..."
      />
      <button
        @click="addTodo"
        class="w-full mt-4 p-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 active:bg-blue-700 transition-all"
      >
        <PlusCircleIcon class="w-10 h-10 mx-auto" />
      </button>
      <ul class="mt-4">
        <li
          v-for="(todo, index) in todos"
          :key="index"
          class="p-2 border border-gray-300 rounded-lg mt-2 flex justify-between items-center"
        >
          <span>{{ todo }}</span>
          <button
            @click="todos.splice(index, 1)"
            class="p-2 bg-red-500 text-white rounded-lg hover:bg-red-600 active:bg-red-700 transition-all"
          >
            <TrashIcon class="w-4 h-4 mx-auto" />
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>
