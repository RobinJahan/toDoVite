<template>
  <div id="app">
    <h1>ToDoVite!</h1>
    <div class="form-todo">
      <input type="text" class="input-todo" placeholder="Ajouter une nouvelle tâche" v-model="newTask" @keydown.enter="addTask">
      <button v-on:click="addTask">Ajouter</button>
    </div>
    <Task v-for="item in toDo"
    :index="item.index"
    :task="item.task"
    :finished="item.finished"
    :key="item.task"
    />
  </div>
</template>

<script>

import Task from './components/Task.vue'


export default {
  name: 'App',
  components: {
    Task
  },
  data() {
    return {
      toDo: [],
      newTask: "",
      numberOfTaskAdded: 0
    }
  },
  mounted(){
    if(localStorage.getItem('toDo')) {
      try {
        this.toDo = JSON.parse(localStorage.getItem('toDo'))
      } catch(e) {
        localStorage.removeItem('toDo')
      }
    }
    if(localStorage.numberOfTaskAdded) {
      this.numberOfTaskAdded = localStorage.numberOfTaskAdded;
    }
  },
  watch:{
    toDo(newToDo) {
      localStorage.toDo = newToDo;
    },
    numberOfTaskAdded(newAdd){
      localStorage.numberOfTaskAdded = newAdd;
    }
  },
  methods: {
    addTask(){
      if (this.newTask.length > 0){
        this.toDo.push({
        index: parseInt(this.numberOfTaskAdded),
        task: this.newTask,
        finished: false
        })
        this.numberOfTaskAdded++
        this.saveTasks()
      }
      this.newTask = ""
    },
    removeTask(index){
      console.log(index)
      this.toDo.splice(this.toDo.findIndex(task => task.index === index),1)
      this.saveTasks()
    },
    changeStateTask(index){
      console.log(index)
      this.toDo[this.toDo.findIndex(task => task.index === index)].finished = !this.toDo[this.toDo.findIndex(task => task.index === index)].finished 
      this.saveTasks()
    },
    saveTasks(){
      const parsed = JSON.stringify(this.toDo)
      localStorage.setItem('toDo', parsed)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 80%;
  margin-left: 10%;
}
h1{
  font-size: 60px;
}
.form-todo{
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}
.form-todo>button{
  font-size: 20px;
}
.input-todo{
  width: 100%;
  height: 30px;
  font-size: 20px;
}
</style>
