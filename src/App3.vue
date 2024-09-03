<script setup>
import {ref, onMounted} from 'vue';

    const name =ref('marcio pain') ;
    const status = ref('active');
    const tasks = ref(['task 1', 'task 2', 'task 3']);
    const newTask = ref('');

    const addTask = () => {
      if(!newTask.value.trim() !== '') {
        tasks.value.push(newTask.value);
        newTask.value = ''
      }
    }

    const deleteTask = (index) => {
      tasks.value.splice(index,1)
    }

    const toggleStatus = () => {
      if(status.value === 'active') {
        status.value = 'pending';
      } else if(status.value === 'pending') {
        status.value = 'inactive';
      } else {
        status.value = 'active';
      }
    }

    onMounted(async () => {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/todos');
        const data = await response.json();
        tasks.value = data.map(title => title.title)
      } catch(error) {
        console.log('error' + error)
      }
    })
</script>

<template>
 <h1>Hello world {{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>
  <form @submit.prevent="addTask">
<label for="newTask">add Task</label>
<br>
<input type="tel" name="newTask" id="addTask" v-model="newTask" />
<input type="submit" value="submit">
  </form>
  <p>tasks:</p>
  <ul>
    <li v-for="task in tasks" :key="task">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>
  <a :href="link">link to google</a>
  <br>
  <button v-on:click="toggleStatus">change status</button>
</template>