<template>

      <div class="text-center">
        <h1>Add a new Task</h1>
        <h4>Get that mental clarity you've been longing for.</h4>
        <p>Today's date is <strong><i>{{ today.toDateString() }}.</i></strong></p>
      </div>

  <div class="container">
    <div class="row justify-content-center align-items-center">
      <div class="col-4">
        <img src="../assets/smartphone.svg" alt="todo app">
      </div>
      <div class="col-4" id="formInputs">
        <input type="text" id="form3Example1" class="form-control" placeholder="Task title" v-model="title" />
        <div>
          <textarea type="text" id="form3Example2" class="form-control" placeholder="Task description"
            v-model="description" />
        </div>
        <div class="d-grid gap-2">
          <button @click.prevent="errorFunction" class="btn btn-primary btn-block text-white mb-4">Add Task</button>
          <p v-if="showErrorMessage" class="alert alert-warning" role="alert">{{ errorMessage }}</p>
        </div>
      </div>
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
// Show current date
const date = new Date('Aug 23 20222');
const currentYear = date.getFullYear();
const currentToday = date.getDate();
const currentMonth = date.getMonth() + 1;
const timeAcross = Date.now();
const today = new Date(timeAcross);
const showErrorMessage = ref(false);
// const constant to save a variable that holds the value of the error message
const errorMessage = ref(null);
const emit = defineEmits(['childEmitTask']);

/* arrow function to call the form holding the task title and task description that uses a conditional to first 
checks if the task title is empty, if true the error message is displayed through the errorMessage container and sets 
a timeOut method that hides the error after some time. Else, its emmits a custom event to the home view with the task 
title and task description; clears the task title and task description input fields.*/
const errorFunction = () => {
  if (title.value.length === 0) {
    showErrorMessage.value = true;
    errorMessage.value = "Your task needs a title to be saved.";
    setTimeout(() => {
      // errorMessage.value = null;
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


<style scoped>
* {
  color: #1a1929;
}

li {
  list-style: none;
}

img {
  padding-top: 0;
  margin-top: 0;
}

h1 {
  font-size: 50px;
  text-transform: uppercase;
}

h1,
h4,
p {
  text-shadow: rgb(200, 200, 200) 0.1em 0.1em 0.1em
}

.container {
  margin-top: 0;
}

.col-4 {
  width: auto;
  align-items: center;
  padding: 0;
}

.text-center {
  margin-top: 20px;
  font-size: large;
}

.alert-warning {
  color: rgb(156, 112, 0);
  text-align: center;
}

#formInputs {
  width: 850px;
}

#form3Example1 {
  margin-bottom: 10px;
}

#form3Example2 {
  margin-bottom: 10px;
  height: 100px;
}
</style>
