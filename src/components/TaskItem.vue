<template>
  <div>
    <div class="container">
      <div class="row justify-content-center">
        <div class="card">
          <div class="card-body">
            <h3 class="card-title">{{ item.title }}</h3>
            <p class="card-text">{{ item.description }}</p>
            <div class="buttons-options">
              <button type="button" class="btn btn-success" @click="completedTask">
                <i class="fa-solid fa-check"></i></button>
              <button type="button" class="btn btn-warning" @click="showEdit"><i
                  class="fa-solid fa-pen-to-square"></i></button>
              <button type="button" class="btn btn-danger" @click="deleteTask"><i
                  class="fa-solid fa-trash-can"></i></button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-if="showEditOptions">
      <form @submit.prevent="editTask">
        <div class="text-center">
          <input type="text" placeholder="Edit title" class="form-control" v-model="taskTitle" />
        </div>
        <div>
          <input type="text" placeholder="Edit description" class="form-control" v-model="taskDescription" />
        </div>
        <input type="submit" class="btn btn-primary btn-block text-white mb-4" value="Edit" />
      </form>
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
  margin-right: 30px;
}

.buttons-options {
  padding-top: 25px
}

i {
  color: white;
}

.form-control {
  width: 500px;
  margin-bottom: 10px;
}

.v-if {
  text-decoration: line-through;
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
</style>
