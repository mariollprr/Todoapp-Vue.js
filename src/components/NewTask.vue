<template>
  <div class="card text-center">
    <div class="card-header">

    </div>
    <div class="card-body">
      <h1 class="card-title">Add a new task</h1>
      <h4>What's on your todo list?</h4>
      <p class="card-text">Today's date is <strong><i>{{ today.toDateString() }}.</i></strong></p>
    </div>
    <div class="card-footer text-muted">
      <div class="alert alert-warning" role="alert" v-if="showErrorMessage" >
        <p>{{ errorMessage }}</p>
      </div>
    </div>
  </div>
  <div class="add-task-section">

    <div class="add-task-form">
      <div class="form-outline mb-4">
        <input type="text" id="form3Example1" class="form-control" placeholder="Task title" v-model="title" />
      </div>
      <div class="form-outline mb-4">
        <input type="text" id="form3Example2" class="form-control" placeholder="Task description" v-model="description" />
      </div>

      <button @click.prevent="errorFunction" class="btn btn-primary btn-block mb-4">Add</button>
    </div>

  </div>
</template>

<script setup>
import { ref } from "vue";
import { useTaskStore } from "../stores/task"
// constant to save a variable that define the custom event that will be emitted to the homeView
const getTask = useTaskStore();
// constant to save a variable that holds the value of the title input field of the new task
const title = ref('');
// constant to save a variable that holds the value of the description input field of the new task
const description = ref('');
/* constant to save a variable that holds an initial false boolean value for the errorMessage container that is 
conditionally displayed depending if the input field is empty*/
const showErrorMessage = ref(false);
// const constant to save a variable that holds the value of the error message
const errorMessage = ref(null);
const emit = defineEmits(['add-task']);
// Show current date
const date = new Date('Aug 23 20222');
const currentYear = date.getFullYear();
const currentToday = date.getDate();
const currentMonth = date.getMonth() + 1;
const timeAcross = Date.now();
const today = new Date(timeAcross);
/* arrow function to call the form holding the task title and task description that uses a conditional to first 
checks if the task title is empty, if true the error message is displayed through the errorMessage container and sets 
a timeOut method that hides the error after some time. Else, its emmits a custom event to the home view with the task 
title and task description; clears the task title and task description input fields.*/
const errorFunction = () => {
  if (title.value.length === 0 || description.value.length === 0) {
    showErrorMessage.value = true;
    errorMessage.value = 'The title or description of your task is empty';
    setTimeout(() => {
      // errorMessage.value = null;
      showErrorMessage.value = false;
    }, 5000);
  } else {
    const newTask = {
      title: title.value,
      description: description.value,
    };
    console.log(newTask);
    emit("add-task", newTask);
    title.value = '';
    description.value = '';
  }
};
</script>


<style scoped>
.form-control {
  width: 60%;
}
.btn {
  padding-right: 57%;
}
</style>
