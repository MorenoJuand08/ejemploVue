<script setup>
import { ref } from 'vue';

  let newTask = ref('')
  let taskList = ref([{text: 'Estudiar', done: false},
   {text: 'Jugar Play', done: true}])

   function setDone(index) {
     taskList.value[index].done = !taskList.value[index].done
   }

  function addTask(){
    if(newTask.value.trim() === '')return
    taskList.value.push({
      text: newTask.value, 
      done: false
    })
    newTask.value = ''
  }

  function deleteTask(index) {
    taskList.value.splice(index, 1)
  }
</script>

<template>
  <div class="card">
    <h1>Lista de cosas</h1>
    <p class="subtitle"> {{newTask}}</p>
    <div>
      <div v-for="(task, index) in taskList" :key="index" class="task" :class="{done: task.done}"> {{ task.text }} <span
        @dblclick="deleteTask(i)" @click="setDone(index)" class="button">x</span> </div>
    </div>
    <div>
      <input v-model="newTask" @keypress.enter="addTask" type="text" placeholder="Escribe tu tarea" />
      <p class="help" v-show="newTask != '' ">Presiona enter para confirmar</p>
    </div>
  </div>
</template>

<style scoped>

.done {
  text-decoration: line-through;
  background-color: #4bee81 !important;
}
.help {
  margin: 5px;
  font-size: 11px;
  opacity: .6;
  text-align: center;
}

input {
  width: 100%;
  box-sizing: border-box;
  border: none;
  outline: none;
  padding: 3px 6px;
  border-radius: 4px;
}


.button:hover{
  cursor: pointer;
  background-color: #023047;
}

.button {
  display: inline-flex;
  background-color: #457b9d;
  padding: 0 5px;
  border-radius: 2px;
  color: white;
  align-items: center;
}

h1 {
  text-transform: uppercase;
  text-align: center;
  padding: 0;
  margin: 0;
  font-size: 24px;
}

.task:hover {
  background-color: #419ce7;
}

.task {
  display: flex;
  justify-content: space-between;
  background-color:#ade8f4 ;
  border-radius: 4px;
  padding: 2px 8px;
  padding-right: 2px;
  margin-bottom: 2px;

}

.subtitle {
  opacity: 60%;
  padding: 0;
  margin: 0;
  text-align: center;
  margin-bottom: 12px;
}

.card {
  font-family: 'Nunito Sans', sans-serif;
  background-color: #afd2da;
  max-width: 520px;
  border-radius: 8px;
  padding: 18px 16px;
  margin: 0 auto;
}

</style>
