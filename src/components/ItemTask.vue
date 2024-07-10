<template>
  <ul id="item">
   <li v-for="task in lista" :key="task.key">
    <span>{{ task.text }}</span>
    <button @click="finishTask(task.key)">Check</button>
   </li>
  </ul>
</template>

<script>
export default {
  name: 'ItemTask',
  props: [
    'lista',
    'delete'
  ],
  methods: {
    finishTask(key) {
      this.delete(key)
    }
  }
}
</script>

<style scoped>
#item {
  white-space: pre-wrap;
  word-wrap: break-word;
  list-style: none;
  padding: 0;
  margin-top: 20px;
}
li {
  padding: 14px;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
}
li:not(:first-child) {
  border-top: 1px solid black;
}
button {
  background-color: #DDD;
  border: 0;
  padding: 8px;
  outline: none;
  border-radius: 4px;
}
</style>