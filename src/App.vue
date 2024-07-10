<template>
  <div id="app">
    <header>Minhas tarefas</header>
    <FormTask />
  </div>
</template>

<script>
import FormTask from './components/FormTask.vue'

export default {
  name: 'App',
  components: {
    FormTask
  }
}
</script>

<style scope>
header {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 80px;
  width: 100%;
  font-size: 40px;
  color: whitesmoke;
}
</style>
