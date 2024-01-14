<script setup>
import { ref } from "vue";

const todos = ref([
  { name: "Task 1", time: 60 },
  { name: "Task 2", time: 90 },
]);

const addTask = ref({ name: "", time: null });

const pushTask = () => {
  if (addTask.value.name == "") {
    alert("Oops, The task input is empty");
  } else if (addTask.value.time == null) {
    alert("Oops, The time input is empty");
  } else {
    todos.value.push(addTask.value);
    addTask.value = {
      name: "",
      time: null,
    };
    isShowing.value = !isShowing.value;
  }
};

const deleteTask = (index) => {
  todos.value.splice(index, 1);
};

// popup
const isShowing = ref(false);
const toggleIsShowing = () => {
  isShowing.value = !isShowing.value;
};
//
</script>

<template>
  <div class="container-sm vh-100 d-flex flex-column justify-content-center ">
    <!-- POPUP DIV -->
    <div
      v-show="isShowing"
      @click="toggleIsShowing()"
      class="popup w-100 z-1 position-absolute start-0 top-0 vh-100"
      style="background: #0000009a"
    >
      <form
        @click.prevent="toggleIsShowing()"
        @submit.prevent=""
        class="container adding-box input-group mt-5 text-start bg-dark py-5 rounded z-2"
      >
        <!-- name input -->
        <div class="name-input w-100 mb-2">
          <label for="nameInp" class="form-label text-white">Task name:</label>
          <input
            v-model="addTask.name"
            type="text"
            placeholder="Type task"
            id="nameInp"
            class="add-task form-control"
          />
        </div>
        <!-- Time input -->
        <div class="time-input w-100 mb-5">
          <label for="timeInp" class="form-label text-white">Time:</label>
          <input
            v-model="addTask.time"
            type="number"
            placeholder="Time"
            id="timeInp"
            class="add-task form-control"
          />
        </div>
        <button @click="pushTask()" class="btn btn-success w-100 rounded">
          Add
        </button>
      </form>
    </div>

    <!-- ///////////////// -->

    <div
      class="bg-dark p-5 rounded position-relative z-0"
     
    >
      <h1 class="text-white mb-2">Assignment - 1</h1>
      <div class="todos-box w-100">
        <ul class="todos list-group w-auto" style="min-width: 320px;">
          <!-- task list item -->
          <li
            v-for="(todo, index) in todos"
            :key="index"
            class="task list-group-item d-flex justify-content-center w-100 position-relative my-2 px-5 overflow-hidden "
          >
            <h3 class="fw-bold position-absolute start-0 ms-2">
              {{ index + 1 }}.
            </h3>
            <h3 class="task-name float-start me-3">{{ todo.name }}</h3>
            <h4 class="time fs-6 font-monospace mt-2 pt-1">
              {{ todo.time }} minutes
            </h4>
            <button
              @click="deleteTask(index)"
              class="delete-task btn btn-danger position-absolute end-0 me-2"
            >
              del
            </button>
          </li>
          <!-- ____________________ -->
        </ul>
      </div>
      <div class="adding-box">
        <button @click="toggleIsShowing()" class="btn btn-warning w-100">
          Add a new task
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
