<template>
<!-- What is v-model in Vue.js? One way to bind data in Vue.js is to use the v-model directive. 
When attached to an input, this model monitors the input and updates the given template once 
there is a change in the model. It also updates the data model if there is a change in the template. 
This is what we call two-way data binding. -->
<form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <!-- v model se bind hugaya text data  -->
      <input type="text" v-model="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
            <!-- v model se bind hugaya day data  -->
      <input
        type="text"
        v-model="day"
        name="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
            <!-- v model se bind hugaya reminder data  -->
      <!-- ye name is the data  -->
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>

    <input type="submit" value="Save Task" class="btn btn-block" />
</form>
</template>


<script>
export default {
  data () {
    return {
        text: '',
        day: '',
        reminder: false,
    }
  },
  methods: {
    onSubmit(event){
        event.preventDefault()

        if(!this.text){
         alert('Please enter a task')
         return;
        }
        const newTask={

        // id: Math.floor(Math.random() * 100000), JSON WILL ADD IT ITSELF.
        text: this.text,
        day: this.day,
        reminder: this.reminder,
        }
        console.log(newTask)
        //Emit upwards to make changes. 
        this.$emit('add-task',newTask)
        
      this.text = ''
      this.day = ''
      this.reminder = false

    }
  },
  
    name: 'addtask'
}

</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>