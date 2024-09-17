<template>

  <form action="" @submit.prevent="addToDo">

    <fieldset role="group" :class="$style.tete">

<input v-model="newTodo" type="text" placeholder="tâches à effectuer" :class="$style.addTask">
<button  :disabled="newTodo.length === 0">Ajouter</button>

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
    <label :class="$style.mask">
      <input type="checkbox" v-model="hideCompleted">
      Masquer les tâches completée
    </label>
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

.completed {
  
  font-size: 35px;
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
  display: flex;
  justify-content: end;
}
.puce {
  display: flex;
  flex-direction: column;
  align-items: center;
  list-style-type: none;
}
</style>