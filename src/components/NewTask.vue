<template>
  <div class="text-center">
    <h1>Add a new Task</h1>
    <h4>Track, visualize and manage tasks in real-time.</h4>
    <p>Today's date is <strong><i>{{ today.toDateString() }}.</i></strong></p>
  </div>
  <div class="container">
    <div class="row justify-content-center align-items-center">
      <div class="col-4">
        <img 
        src="../assets/smartphone.svg" 
        alt="todo app"
        />
      </div>
      <div class="col-4" id="formInputs">
        <input 
        type="text" 
        id="form3Example1" 
        class="form-control" 
        placeholder="Task title"
         v-model="title" />
        <div>
          <textarea 
          type="text" 
          id="form3Example2" 
          class="form-control"
          placeholder="Task description"
          v-model="description"
          />
        </div>
        <div class="d-grid gap-2">
          <p v-if="showErrorMessage" class="alert alert-warning" role="alert">{{ errorMessage }}</p>
          <button @click.prevent="errorFunction" class="btn btn-primary btn-block text-white mb-4">Add Task</button> 
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
// const constant to save a variable that holds the value of the error message
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
  width: 750px;
}

#form3Example1 {
  margin-bottom: 10px;
}

#form3Example2 {
  margin-bottom: 10px;
  height: 100px;
}
</style>
