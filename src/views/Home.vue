<template>
<Nav/>
<NewTask @childEmitTask="addTask" />
<TaskItem 
    v-for="task in useTaskStore().tasks"
    :key="task.id"
    :item="task"
    @childToggleStatus="completedTask"
    @childEditStatus="editTask"
    @childDeleteStatus="deleteTask"
  />
<Footer/>
<div class='ripple-background'>
  <div class='circle xxlarge shade1'></div>
  <div class='circle xlarge shade2'></div>
  <div class='circle large shade3'></div>
  <div class='circle mediun shade4'></div>
  <div class='circle small shade5'></div>
</div>
</template>

<script setup>
import Nav from "../components/Nav.vue";
import NewTask from "../components/NewTask.vue";
import TaskItem from "../components/TaskItem.vue"
import Footer from "../components/Footer.vue";
import { useTaskStore } from "../stores/task";

useTaskStore().fetchTasks();
const addTask = async (newTask) => {
  const res = await useTaskStore().addTask(newTask.title, newTask.description);
  useTaskStore().fetchTasks();
};
const completedTask = async (id, booleanValue) => {
  booleanValue = !booleanValue;
  const res = await useTaskStore().completedTask(id, booleanValue);
  useTaskStore().fetchTasks();
};
const editTask = async (newTask) => {
  const res = await useTaskStore().editTask(
    newTask.title,
    newTask.description,
    newTask.id
  );
  useTaskStore().fetchTasks();
};
const deleteTask = async (id) => {
  const res = await useTaskStore().deleteTask(id);
  useTaskStore().fetchTasks();
};
</script>

<style>
Footer {
  position:fixed;
  bottom: 0;
}
</style>

