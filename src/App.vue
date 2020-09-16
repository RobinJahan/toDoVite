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
  methods: {
    addTask(){
      if (this.newTask.length > 0){
        this.toDo.push({
        index: this.numberOfTaskAdded,
        task: this.newTask,
        finished: false
        })
        this.numberOfTaskAdded++
      }
      this.newTask = ""
    },
    removeTask(index){
      this.toDo.splice(this.toDo.findIndex(task => task.index === index),1)
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
