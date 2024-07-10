<template>
  <div id="task">
    <form @submit.prevent="addTaskItem">
      <input 
        type="text" 
        placeholder="Digite sua tarefa.."
        v-model='tarefa' 
      >

      <button type="submit">Adicionar</button>
    </form>

    <ItemTask :lista="tarefas" :delete="deleteTaskItem"/>

    <div v-if="tarefas.length" class="text-quantidade">
      Você tem <strong :class="{pendente: tarefas.length > 4}">{{ tarefas.length }}</strong> tarefas restantes.
    </div>
  </div>
</template>

<script>
import ItemTask from './ItemTask'

export default {
  name: 'FormTask',
  components: {
    ItemTask,
  },
  data() {
    return {
      tarefa: '',
      tarefas: []
    }
  },
  methods: {
    addTaskItem() {
      if(this.tarefa !== '') {
        this.tarefas.push({
          text: this.tarefa,
          key: Date.now()
        })
      } else {
        alert('Digite uma tarefa..')
        return
      }

      this.tarefa = ''
    },
    deleteTaskItem(key) {
      let filtro = this.tarefas.filter( (item) => {
        return (item.key !== key)
      })

      return this.tarefas = filtro
    }
  },
  watch: {
    tarefas: {
      deep: true,
      handler() {
        localStorage.setItem('task', JSON.stringify(this.tarefas))
      }
    }
  },
  created() {
    const json = localStorage.getItem('task')
    this.tarefas = JSON.parse(json) || []
  }
}
</script>

<style scoped>
#task {
  max-width: 700px;
  background: #FFF;
  border-radius: 4px;
  padding: 20px;
  margin: 20px;
  box-shadow: 0 0 20px rgba(0,0,0,0.3);
}

form {
  display: flex;
  flex-direction: row;
  margin-top: 30px;
}

button {
  cursor: pointer;
  background-color: #0f5959;
  color: #FFF;
  text-transform: uppercase;
  font-weight: 600;
  padding: 0 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 10px;
  border-radius: 4px;
}

input {
  flex: 1;
  padding: 6px 10px;
  border-radius: 4px;
}

.pendente {
  color: red;
}
</style>