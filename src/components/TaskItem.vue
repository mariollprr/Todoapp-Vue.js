<template>
    <div class="container">
      <div class="row justify-content-center align-items-center">
        <div class="card">
          <div class="card-body">
            <h3 class="card-title">{{ item.title }}</h3>
            <p class="card-text">{{ item.description }}</p>
            <div class="buttons-options">
              <button type="button" class="btn btn-success" data-bs-toggle="tooltip" data-bs-placement="top" title="Mark as complete"
 @click="completedTask">
                <span v-if="!isCompleted" style=".card-title, .card-text {text-decoration: line-through;}" class="material-symbols-outlined">
                  radio_button_unchecked
                </span>
                <span v-else class="material-symbols-outlined">
                  check_circle
                </span>
              </button>
              <button type="button" class="btn btn-warning" data-bs-toggle="tooltip" data-bs-placement="top" title="Edit" @click="showEdit">
                <i class="fa-solid fa-pen-to-square"></i>
              </button>
              <button type="button" class="btn btn-danger" data-bs-toggle="tooltip" data-bs-placement="top" title="Delete" @click="deleteTask">
                <i class="fa-solid fa-trash-can"></i>
              </button>
            </div>
          </div>
        </div>
      </div>
    <div class="container" v-if="showEditOptions">
      <div class="row justify-content-center align-items-center">
        <div >
        </div>
        <div id="formInputs2">
          <form @submit.prevent="editTask">
            <input 
            type="text" 
            id="form3Example20" 
            class="form-control" 
            placeholder="Edit title" 
            v-model="taskTitle" 
            />
            <div>
              <textarea 
              type="text" 
              id="form3Example21" 
              class="form-control" 
              placeholder="Edit description"
              v-model="taskDescription"
               />
            </div>
            <div class="d-grid gap-2">
              <button 
              type="submit" 
              id="btnEdit" 
              class="btn btn-warning btn-block text-white mb-4">
              Edit Task
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
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
  margin-right: 40px;
}

.buttons-options {
  padding-top: 25px;
}

i {
  color: white;
}

.btn-success {
  padding: 0px;
  padding-top:7px;
}

.card {
  justify-content: center;
  display: flex;
  width: 700px;
  height: max-content;
  color: #2f2e41;
  background-color: #f4fbff;
  border-radius: 20px;
  margin: 20px 15px;
  border-left: solid cornflowerblue 5px;
  -webkit-box-shadow: 6px 6px 5px 0px rgba(212, 212, 212, 1);
  -moz-box-shadow: 6px 6px 5px 0px rgba(212, 212, 212, 1);
  box-shadow: 6px 6px 5px 0px rgba(212, 212, 212, 1);
}

.form-control {
  display:grid;
  align-items: center;
  flex-direction: row;
  margin:10px auto;
  color: #2f2e41;
  background-color: #fff2a8;
  border-radius: 20px;
  border-left: solid rgb(246, 221, 0) 5px;
  -webkit-box-shadow: 6px 6px 5px 0px rgba(212, 212, 212, 1);
  -moz-box-shadow: 6px 6px 5px 0px rgba(212, 212, 212, 1);
  box-shadow: 6px 6px 5px 0px rgba(212, 212, 212, 1);
}


#btnEdit {
  width: 220px;
  margin: 0;
}

#formInputs2 {
  width: 500px;
}

#form3Example21 {
  margin-bottom: 10px;;
  height: 150px;
}



</style>
