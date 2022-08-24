<template>
  <div class="card text-center">
    <div class="container">
      <div class="container-card card-body">
        <h1 class="card-title">Add a new Task</h1>
        <h4>What's on your todo list?</h4>
        <p class="card-text">Today's date is <strong><i>{{ today.toDateString() }}.</i></strong></p>
      </div>
      <div class="container-svg">
        <img src="../assets/todo-girl.svg" alt="Girl task">
      </div>
    </div>
   
      <div class="alert alert-danger" role="alert" v-if="showErrorMessage">
        <p>{{ errorMessage }}</p>
      </div>
    
  </div>

  <div class="container">
    <div class="form-outline container-card-center mb-4 shadow-3">
      <input type="text" id="form3Example1" class="form-control shadow-3" placeholder="Task title" v-model="title" />
    </div>
    <div class="form-outline mb-4">
      <input type="text" id="form3Example2" class="form-control shadow-3" placeholder="Task description" v-model="description" />
    </div>
    <button @click="getInfo" class="btn btn-primary btn-block text-white mb-4">Add Task</button>
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
const emit = defineEmits(['childEmitTask']);
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
const getInfo = async () => {
  if (title.value.length > 0) {
    const task = {
      title: title.value,
      description: description.value,
    };
    emit("childEmitTask", task);
    title.value = "";
    description.value = "";
  } else {
    errorMsg.value = "Error: Title is required";
    setTimeout(() => {
      errorMsg.value = null;
    }, 5000);
  }
};

</script>


<style scoped>
* {
  color: #1a1929;
}

.container {
  display: flex;
  align-items: center;
}

.container-svg {
  padding-right: 80px;
}

.form-control {
  width: 60%;
}

.form-outline {
  display: inline-block;
}


.add-task-form {
  justify-content: center;
  align-items: center;
  position: relative;
}
</style>
