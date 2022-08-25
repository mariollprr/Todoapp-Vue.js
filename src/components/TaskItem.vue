<template>
  <div>
    <div class="card">
      <div class="card-body">
        <h3 class="card-title">{{ item.title }}</h3>
        <p class="card-text">{{ item.description }}</p>
        <div class="buttons-options">
          <button type="button" class="btn btn-success" @click="completedTask"><i
              class="fa-solid fa-circle-check"></i></button>
          <button type="button" class="btn btn-warning" @click="showEdit"><i
              class="fa-solid fa-pen-to-square"></i></button>
          <button type="button" class="btn btn-danger" @click="deleteTask"><i class="fa-solid fa-trash"></i></button>
        </div>
      </div>
    </div>
    <div v-if="showEditOptions">
      <form @submit.prevent="editTask">
        <div class="edit-inputs">
          <input type="text" placeholder="Edit title" class="form-control" v-model="taskTitle" />
        </div>
        <div>
          <input type="text" placeholder="Edit description" class="form-control" v-model="taskDescription" />
        </div>
        <input type="submit" class="btn btn-primary btn-block text-white mb-4" value="Edit" />
      </form>
    </div>
  </div>
  <!-- 
  <p v-if="!isCompleted">To Do</p>
  <p v-else>Complete</p> -->
</template>

<script setup>
import { ref, defineProps } from "vue";
import { useTaskStore } from "../stores/task"

const taskTitle = ref("");
const taskDescription = ref("");
const showEditOptions = ref(false);
const isCompleted = ref(false);
const emit = defineEmits([
  "childEditStatus",
  "childToggleStatus",
  "childDeleteStatus",
]);

const props = defineProps(["item"]);
const showEdit = () => {
  showEditOptions.value = !showEditOptions.value;
};

const editTask = () => {
  const newTask = {
    title: taskTitle.value,
    description: taskDescription.value,
    id: props.item.id,
  };
  emit("childEditStatus", newTask);
  (taskTitle.value = ""), (taskDescription.value = "");
};

const completedTask = (id) => {
  isCompleted.value = !isCompleted.value;
  emit("childToggleStatus", props.item.id);
};

const deleteTask = () => {
  emit("childDeleteStatus", props.item.id);
};

</script>

<style scoped>
button {
  height: 40px;
  width: 40px;
  padding-right: 20px;
  margin-right: 20px;
}

.buttons-options {
  padding-top: 30px
}

i {
  color: white;
}

.form-control {
  width: 600px;
  margin-bottom: 10px;
}

.v-if {
  text-decoration: line-through;
}

.card {
  display: flex;
  width: 500px;
  height: max-content;
  background-color: #f4fbff;
  border-radius: 20px;
  margin-left: 20px;
  margin-bottom: 20px;
  border-left: solid cornflowerblue 5px;
  -webkit-box-shadow: 6px 6px 5px 0px rgba(212, 212, 212, 1);
  -moz-box-shadow: 6px 6px 5px 0px rgba(212, 212, 212, 1);
  box-shadow: 6px 6px 5px 0px rgba(212, 212, 212, 1);
}

</style>


<!-- 
**Hints**
1. ref() or reactive() can be used here to store the following, think if you want to store them either individually or like an object, up to you.
2. Data properties need here are the following: a boolean to store a false**Important variable, a string to store an error, a string to store the value of the task that the user can edit, an initial false boolean to hide the inputFIeld used to edit the new task detail or details[this is in reference of the task title and the task description].
3. Store the custom emit events that will be used to call the functions of the homeView for editing, deleting and toggling the status[completed, not complted] of the taskItem.
4. Function to handle the error with the data properties used to control the error and the the boolean controlling the boolean empty variable.
5. Function to handle the edit dialogue where the inputField is displayed and the string used to store the value of the inputField will be used here to save the value as a prop on this function.
6. Function to emmit a custom event emit() that takes 2 parameters a name for the custom event and the value that will be send via the prop to the parent component. This function can control the toggle completion of the task on the homeview.
7. Function to edit the task information that you decided that the user can edit. This function's body takes in a conditional that first checks if the value of the task [either title and description or just title] is empty which if true it runs the function used to handle the error on hint4. Else, the conditional sets the first mentioned boolean data property on hint2 back to its inital boolean value to hide the error message and repeat the same for the data property mentioned 4th on hint2; a constant that stores an object that holds the oldValue from the prop item and the value of the task coming from the data property mentioned 3rd on hint2; a custom event emit() that takes 2 parameters a name for the custom event and the value from the object used on this part of the conditional and lastly this part of the conditional sets the value of input field to an empty string to clear it from the ui. 
8. Function to emmit a custom event emit() that takes 2 parameters a name for the custom event and the value that will be send via the prop to the parent component. This function can control the removal of  the task on the homeview.
-->
