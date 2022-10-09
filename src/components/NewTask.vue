<template>
  <div class="">
    <h1>Add a new Task</h1>
    <h4>Track, visualize and manage tasks in real-time.</h4>
    <p>Today's date is <strong><i>{{ today.toDateString() }}.</i></strong></p>
  </div>
  <div class="">
    <div class="">
      <div class="">
      </div>
      <div class="" id="formInputs">
        <input 
        type="text" 
        id="form3Example1" 
        class="" 
        placeholder="Task title"
         v-model="title" />
        <div>
          <textarea 
          type="text" 
          id="form3Example2" 
          class=""
          placeholder="Task description"
          v-model="description"
          />
        </div>
        <div class="">
          <p v-if="showErrorMessage" class="" role="alert">{{ errorMessage }}</p>
          <button @click.prevent="errorFunction" class="">Add Task</button> 
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useTaskStore } from "../stores/task"


const getTask = useTaskStore();
const title = ref('');
const description = ref('');

// Show current date
const date = new Date('Aug 23 20222');
const currentYear = date.getFullYear();
const currentToday = date.getDate();
const currentMonth = date.getMonth() + 1;
const timeAcross = Date.now();
const today = new Date(timeAcross);

// Error message
const showErrorMessage = ref(false);

// Constant to save a variable that holds the value of the error message
const errorMessage = ref(null);
const emit = defineEmits(['childEmitTask']);

const errorFunction = () => {
  if (title.value.length === 0) {
    showErrorMessage.value = true;
    errorMessage.value = "Your task needs a title to be saved.";
    setTimeout(() => {
      showErrorMessage.value = false;
    }, 5000);
  } else {
    const newTask = {
      title: title.value,
      description: description.value,
    };
    emit("childEmitTask", newTask);
    title.value = "";
    description.value = "";
  }
};

</script>


<style></style>
