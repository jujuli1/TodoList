<template>

  <form action="" @submit.prevent="addToDo">

    <fieldset role="group" :class="$style.tete">

<input v-model="newTodo" type="text" placeholder="tâches à effectuer" :class="$style.addTask">
<button  :disabled="newTodo.length === 0">Ajouter</button>

<label :class="$style.mask">
      <input type="checkbox" v-model="hideCompleted">
      Masquer les tâches completée
    </label>

</fieldset>

  </form>
  
  <div v-if = "todos.length === 0">Vous n'avez pas de tâches à faire</div>
  <div v-else>

    <ul :class="$style.puce">

      <li v-for="todo in sortedTodos()" :key="todo.date" :class="$style.completed">

        <label>

          <input type="checkbox" v-model = "todo.completed">
        </label>
        {{ todo.title }}

      </li>
    </ul>

    <div :class="$style.container">

      <div :class="$style.cup">

        <div :class="$style.top">
          <div :class="$style.vapour">
            <span style="--i:1;"></span>
            <span style="--i:3;"></span>
            <span style="--i:16;"></span>
            <span style="--i:5;"></span>
            <span style="--i:13;"></span>
            <span style="--i:20;"></span>
            <span style="--i:6;"></span>
            <span style="--i:7;"></span>
            <span style="--i:10;"></span>
            <span style="--i:8;"></span>
            <span style="--i:17;"></span>
            <span style="--i:11;"></span>
            <span style="--i:12;"></span>
            <span style="--i:14;"></span>
            <span style="--i:2;"></span>
            <span style="--i:9;"></span>
            <span style="--i:15;"></span>
            <span style="--i:4;"></span>
            <span style="--i:19;"></span>
            
            
          </div>
          <div :class="$style.circle">
            <div :class="$style.tea"></div>
          </div>
        </div>
      </div>
    </div>
    
  </div>
</template>

<script setup>
import {ref} from 'vue'

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  {title: "tache de test",
    completed: true,
    date: 1,


  },

  {title: "tache à faire",
    completed: false,
    date: 2,


  },



])

const addToDo = () => {
  todos.value.push({
    title: newTodo.value,
    completed: false,
    date: Date.now()
  })

  newTodo.value = ''
}

const sortedTodos = () => {
  const sortedTodos =  todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)

if(hideCompleted.value === true){
  return sortedTodos.filter(t => t.completed === false)
}
return sortedTodos
}


</script>

<style module>

body {
  
  
  min-height: 100vh;
  background: #607d8b;
}

.container {
  position: relative;
  top: 50px;
}
.cup
{
  position: relative;
  width: 280px;
  height: 300px;
  background: linear-gradient(to right, #f9f9f9, #d9d9d9);
  border-bottom-left-radius: 45%;
  border-bottom-right-radius: 45%;
}

.top {
  position: absolute;
  top: -30px;
  left: 0;
  width: 100%;
  height: 60px;
  border-radius: 50%;
  background: linear-gradient(to right, #f9f9f9, #d9d9d9);
}

.circle{
  position: absolute;
  top: 5px;
  left: 10px;
  width: calc(100% - 20px);
  height: 50px;
  border-radius: 50%;
  box-sizing: border-box;
  background: linear-gradient(to left, #f9f9f9, #d9d9d9);
  overflow: hidden;
}

.tea{
  position: absolute;
  top: 20px;
  left:0;
  width: 100%;
  height: 100%;
  background: linear-gradient(#5fd15f, #008000);
  border-radius: 50%;


}

.vapour {
  position: relative;
  display: flex;
  z-index: 1;
  padding: 0 20px;
}

.vapour span {
  position: relative;
  bottom:50px;
  display: block;
  margin: 0 2px 50px;
  min-width: 8px;
  height: 120px;
  background: #fff;
  border-radius: 50%;
  animation: animate 5s linear infinite;
  filter: blur(8px);
  animation-delay: calc(var(--i) * -0.5s);
}

@keyframes animate {
  0%
  {
    transform: translateY(0) scaleX(1);
    opacity: 0

  }
  15%
  {
    opacity: 1;
  }
  50%
  {
    transform: translateY(-150px) scaleX(5)
  }
  95%
  {
    opacity: 0;
  }
  100%
  {
    transform: translateY(-30px0) scaleX(10)
  }
}

.completed {
  
  font-size: 35px;
  margin-top: 80px;
  margin-bottom: 20px;
  opacity: 0;  
  animation: fadeIn 2s forwards; 
}

@keyframes fadeIn {
  from {
    opacity: 0; 
    font-size: 40px;
  }
  to {
    opacity: 1;
    font-size: 35px;  
  }
}

.addTask {
  border-radius: 5rem;
  width: 20rem;
  margin-top: 15px;
  margin-left: 29px;
}
.tete {
  background-color: aqua;
  border-radius: 5rem;
  height: 50px;
}

.mask {
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  font-size: 20px;
  display: flex;
  justify-content: end;
  margin-top: -25px;
  margin-right: 50px;
}
.puce {
  display: flex;
  flex-direction: column;
  align-items: center;
  list-style-type: none;
}
</style>