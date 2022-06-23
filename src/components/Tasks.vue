<template>
<!-- Loop thru the prop tasks  -->
<!--  -->
<div  v-bind:key="task.id" v-for="task in tasks">
    <h3>
                <!-- SEDNING INDIVIDUAL TASK OBJECT -->
        <Task @toggle-reminder="$emit('toggle-reminder' , task.id)" @delete-task="$emit('delete-task' , task.id)" :task="task"/>
        <!-- this will emit up one level -->

    </h3>

</div>
</template>


<script>
import Task from './TheTask.vue'

export default {
  props: {
    tasks:Array
  },
    components:{
        Task,
    },
  name: 'Tasks',
  emits:['delete-task' , 'toggle-reminder'],
}
</script>