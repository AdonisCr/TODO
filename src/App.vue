<script setup lang="ts">
import { ref } from 'vue';

// Référence pour stocker la tâche entrée par l'utilisateur
const newTask = ref<string>('');

// Référence pour stocker toutes les tâches
const tasks = ref<{ text: string, completed: boolean }[]>([]);

// Fonction pour ajouter une nouvelle tâche
const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push({ text: newTask.value, completed: false });
    newTask.value = ''; // Réinitialiser l'input après ajout
  }
};

// Fonction pour marquer une tâche comme complétée
const markTaskAsCompleted = (index: number) => {
  tasks.value[index].completed = !tasks.value[index].completed;
};
</script>

<template>
  <div class="container">
    <h3>TO DO LISTE</h3>
    <div class="input">
      <input type="text" v-model="newTask" placeholder="Saisir une tâche"> 
      <input type="submit" @click="addTask" value="Submit">
    </div>
    <div class="save">
      <ul>
        <li v-for="(task, index) in tasks" :key="index" :class="{ completed: task.completed }">
          {{ task.text }}
          <button @click="markTaskAsCompleted(index)">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" style="fill:lightcoral ;">
              <path d="M5 20a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V8h2V6h-4V4a2 2 0 0 0-2-2H9a2 2 0 0 0-2 2v2H3v2h2zM9 4h6v2H9zM8 8h9v12H7V8z"></path>
              <path d="M9 10h2v8H9zm4 0h2v8h-2z"></path>
            </svg>
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.container {
  width: 50%;
  height: 100vh;
  background-color: rgb(240, 240, 240);
  margin: auto;
  border: solid 0.2px darkgrey;
  align-items: center;
  text-align: center;
} 

.input {
  display: flex;
  gap: 20px;
  justify-content: center;
  margin-top: 20px;
}

.save ul {
  list-style-type: none;
  padding: 0;
}

.save li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

button {
  padding: 5px 10px;
  border: none;
  background-color: transparent;
  cursor: pointer;
}

button svg {
  fill: lightcoral;
}

.completed {
  text-decoration: line-through;
  color: grey;
}
</style>
