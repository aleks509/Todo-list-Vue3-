<script setup>
import { ref, computed } from "vue";

const todoText = ref("");
const todoList = ref([]);
const pendingTask = computed(() => {
  return todoList.value.filter((item) => !item.checked);
});

const complitedTask = computed(() => {
  return todoList.value.filter((item) => item.checked);
});

function clearTask() {
  todoText.value = "";
}

function addTask() {
  if (todoText.value && todoText.value !== "") {
    todoList.value.push({
      id: new Date().valueOf(),
      name: todoText.value,
      checked: false,
    });
    clearTask();
  }
}
</script>

<template>
  <div class="todo-container w3-white w3-card-4">
    <!-- Header-->
    <div class="w3-container w3-black w3-margin-0 w3-bottombar w3-border-blue">
      <h1>
        <i class="fa-solid fa-clipboard-list"></i>
        To-Do List
      </h1>
    </div>
  
  <!-- User input  -->
  <div class="w3-container flex-container w3-light-gray w3-padding">
    <input
      class="w3-input w3-border-0"
      type="text"
      autofocus
      v-model="todoText"
      @keyup.enter="addTask()"
      placeholder="Type here your super task..."
    />
    <button class="w3-button w3-gray" @click="clearTask()">
      <i class="fa-solid fa-times"></i>
    </button>
    <button class="w3-button w3-blue" @click="addTask()">
      <i class="fa-solid fa-plus"></i>
    </button>
  </div>
  <!-- List of pending tasks -->
  <div class="w3-padding w3-blue">Pending: {{ pendingTask.length }}</div>
  <div class="w3-padding" v-for="task in pendingTask" :key="todoList.id">
    <label>
      <input type="checkbox" v-model="task.checked" />
      <span class="w3-margin-left">{{ task.name }}</span>
    </label>
  </div>
  <div class="w3-padding" v-show="pendingTask.length == 0">No tasks</div>
  <!-- List of completed tasks -->
  <div class="w3-padding w3-blue">Completed {{ complitedTask.length }}</div>
  <div class="w3-padding" v-for="task in complitedTask" :key="todoList.id">
    <label>
      <input type="checkbox" v-model="task.checked" />
      <span class="w3-margin-left">{{ task.name }}</span>
    </label>
  </div>
  <div class="w3-padding" v-show="complitedTask.length == 0">No tasks</div>
</div>
</template>
