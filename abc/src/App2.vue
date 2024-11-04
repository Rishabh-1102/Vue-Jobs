import { onMounted } from 'vue';

<script>
  export default{
    data(){
      return {
        name: 'John Dow',
        status: false,
        tasks: ['Task1','Task2','Task3'],
        link : 'https://google.com',
        newTask : ('')
      }
    },
    methods: {
      toggleStatus(){
        if(this.status===true){
          this.status = false;
        }
        else if(this.status === false){
          this.status = true;
        }
      },
      addTask() {
        if(this.newTask.trim() !== ''){
          this.tasks.push(this.newTask);
          this.newTask = '';
        }
      },
      deleteTask(index){
        this.tasks.splice(index,1);
      }
    },
    async onMounted() {
      try{
        const res = await fetch('https://jsonplaceholder.typicode.com/todos')
        const data = await res.json();
        this.tasks = data.map(task => task.title);
      }catch(error){
        console.log(error)
      }
    }
  }
</script>

<template>
  <div>
    <h1>{{ name }}</h1>
    <p v-if="status">User is active</p>
    <p v-else>User is inactive</p>
    <h3>Tasks:</h3>
    <ul>
      <li v-for="{task,index} in tasks" :key="task">
        <span>
          {{ task }}
        </span>
        <button @click="deleteTask(index)">X</button>
      </li>
    </ul>
    <a :href="link">Click here</a>

    <button v-on:click="toggleStatus">Change status</button>

    <form @submit.prevent="addTask">
      <label for="newTask">Add Task</label>
      <input type="text" name="newTask" id="newTask" v-model="newTask">
      <button type="submit" @click="addTask">Submit</button>
    </form>
  </div>
</template>



