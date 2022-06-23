<template>
  <header>
    <h1> {{title}}</h1>
    <Button v-show="homePage"  @btn-click="$emit('toggle-add-task')" v-bind:text="showAddTask ? 'Close' : 'Add Task'" :color="showAddTask ? 'Red' : 'Green'"/>
  </header>
</template>

<script>
import Button from './TheButton.vue'
export default {
  data () {
    return {
    }
  },
  methods: {
  },
  computed:{
    homePage(){ //SHOW ADD TASK BUTTON ONLY ON HOME ROUTE
      if(this.$route.path==='/'){
        return true
      }
      else{
        return false
      }

    }
  },
  props: {
    showAddTask:Boolean,
    title:{
      type:String,
      default:'NO PROPS FOUND!'
    }
  },
  components: {
    Button
  },
  name: 'TheHeader',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped> 
header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
  align-items: center;
}
</style>
