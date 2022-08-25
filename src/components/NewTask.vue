<template>
  <div>
    <div>
      <div class="text-center">
        <h1>Add a new Task</h1>
        <h4>-Get that mental clarity you've been longing for.</h4>
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
              <input type="text" id="form3Example2" class="form-control" placeholder="Task description" v-model="description" />
            </div>
            <button @click="getInfo" class="btn btn-primary btn-block text-white mb-4">Add Task</button>
          </div>
        </div>
      </div>
    </div>

    <div class="alert alert-danger" role="alert" v-if="showErrorMessage">
      <p>{{ errorMessage }}</p>
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
    errorMessage.value = "The title or description of your task is empty";
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

li {
  list-style: none;
}

img {
  padding-top: 0;
  margin-top: 0;
}

h1 {
  font-size: 60px;
}
h1, h4, p {
  text-shadow: rgb(200, 200, 200) 0.1em 0.1em 0.1em
  }
.container {
  margin-top: 0;
}

.col-4 {
  width: auto;
  align-items: center;
}

.text-center {
  margin-top: 20px;
  font-size: large;
}
#formInputs {
  width: 600px;
}

#form3Example1 {
  margin-bottom: 5px;
}

#form3Example2 {
  margin-bottom: 5px;
}
</style>
