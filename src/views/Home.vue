<template>
 <div v-show="showAddTask">
   <!-- The v-show directive is a Vue.js directive used to toggle the display CSS property of a element with our data. 
  If the data is true it will make it visible else it will make it invisible. -->
  <AddTask @add-task="addNewTask"/>

  </div>
  <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask " v-bind:tasks="tasks"/> 
  <!-- Agar mkabhi tasks change hua tou v bind -->

</template>

<script>
import Tasks from '../components/Tasks'
import AddTask from '../components/AddTask'

export default { 
  props: {
    showAddTask:Boolean,
  },
  methods: {
    //---------------------------------------------------------------------------------------------------//

    async fetchTask(id){ //Fetch a single task for toggle reminder.
      const res = await fetch(`http://localhost:5000/tasks/${id}`)
      const data=await res.json()
      return data
    },

    //---------------------------------------------------------------------------------------------------//
    async addNewTask(newTask){
      const res = await fetch("http://localhost:5000/tasks" , {
        method:'POST',
        headers:{
          'Content-type':'application/json',
     
        },
          body:JSON.stringify(newTask)
      })
      const data=await res.json()
      this.tasks=[...this.tasks,data]

    },

    //-------------------------------------Map returns an array of updated tasks-----------------------//
    async toggleReminder(id){
      const taskToToggle=await this.fetchTask(id)
      
      const updatedTasks={...taskToToggle, Reminder:!taskToToggle.Reminder}
      const res = await fetch(`http://localhost:5000/tasks/${id}` , {
        method:'PUT', // forupdate.
        headers:{
          'Content-type':'application/json',
     
        },
        body:JSON.stringify(updatedTasks)

      })
      const data=await res.json()
      console.log("THIS IS MY " , data)



      this.tasks=this.tasks.map((task)=>task.id===id ? { 
        ...task,Reminder:data.Reminder
      } :task )

    },
    //---------------------------------------------------------------------------------------------------//
    async deleteTask(id){

      if(confirm ( 'Are you sure? ')){
          const res = await fetch(`http://localhost:5000/tasks/${id}` , {
            method:'DELETE',

          })
          res.status===200 ? this.tasks=this.tasks.filter((task)=>task.id !==id) : alert('ERROR DELETING.')
      }

    //---------------------------------------------------------------------------------------------------//
    },
    async fetchTasks(){
      const res = await fetch('http://localhost:5000/tasks')
      const data=await res.json()
      return data
    },
     //---------------------------------------------------------------------------------------------------
  },
    data () {
        return {
            tasks:[],
        }
    },
    async created(){
        this.tasks=await this.fetchTasks()
        console.log(this.tasks)

    },

    name:'Home',
    components:{
        Tasks,
        AddTask,
    },   
   

}
</script>