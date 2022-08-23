<template>
<Nav/>
<NewTask/>
<TaskItem/>
<Footer/>

</template>

<script setup>
import Nav from "../components/Nav.vue";
import NewTask from "../components/NewTask.vue";
import TaskItem from "../components/TaskItem.vue"
import Footer from "../components/Footer.vue";
</script>

<style>
html {
  min-height: 100%;
  position: relative;
}
body {
  margin: 0;
  margin-bottom: 40px;
}
Footer {
  position: absolute;
}
</style>

