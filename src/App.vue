<template>
  <div class="container">
     <Header title="Task Tracker" @toggle-add-task="toggleAddTask" :showAddTask="showAddTask"/>
     <div class="" v-show="showAddTask">
       <AddTask @add-task="addTask"/>
     </div>
     <Tasks @delete-task="deleteTask" @toggle-reminder="setReminder" :tasks="tasks" />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'


export default {
  name: 'App',
  components: {
    Header,Tasks,AddTask
    
  },
  data(){
    return {
      tasks:[],
      showAddTask:false,
    
    }
  },
  methods: {
   async deleteTask(id){

        if(confirm('Are you sure, you want to delete? ')){
          const res = await fetch(`api/tasks/${id}`,{
              method:'DELETE',
              headers:{
                'Content-type':'application/json',
              },
              // body: JSON.stringify(task)
            });
          
            res.status ===200 ?  this.fetchTasks() : alert("error deleting task")
            
            // (this.tasks = this.tasks.filter((task)=> task.id !=id) )
        }
      
    },
  async setReminder(id){
      // this.tasks = this.tasks.map((task)=> task.id == id ? {...task, reminder:!task.reminder} : task)
      const taskToUpdate = await this.fetchTask(id);
      console.log("apa 2")
      console.log(taskToUpdate);
      
      // const updateTask = {...taskToUpdate, reminder:!taskToUpdate.reminder}
      // console.log(updateTask);
      // const res = await fetch(`api/tasks/${id}`,{
      //         method:'PUT',
      //         headers:{
      //           'Content-type':'application/json',
      //         },
      //         body: JSON.stringify(updateTask)
      //       });

      //       const data = await res.json();
      //       console.log(data);
          
      //       res.status ===200 ?  this.fetchTasks() : alert("error updating task")
    },
    async addTask(task){
      // this.tasks.push(task);
    
      const res = await fetch('api/tasks',{
        method:'POST',
        headers:{
          'Content-type':'application/json',
        },
        body: JSON.stringify(task)
      });
    
      const data = await res.json();
      this.tasks = [...this.tasks,data]
      // this.fetchTasks();
    },
    toggleAddTask(){
      this.showAddTask = !this.showAddTask 
    },
    async fetchTasks(){
      const res = await fetch("api/tasks");
      this.tasks=await res.json();
    },
    async fetchTask(id){
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      console.log("apa");
      console.log(data);
      return  data;
    }
  },
  created(){
    this.fetchTasks();
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>