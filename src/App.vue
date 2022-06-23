<template>
<div class="container">

  <Header  :showAddTask="showAddTask" @toggle-add-task="toggleAddTask" title='Task Tracker'  />
  <!-- as props to home  -->
  <router-view :showAddTask="showAddTask"></router-view> 

  <Footer/>
</div>

</template>
<script>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'


export default {
  methods: {
    //---------------------------------------------------------------------------------------------------//
    toggleAddTask(){
      this.showAddTask=!this.showAddTask
    },
    //---------------------------------------------------------------------------------------------------//   
  },
  data () {
    return { //Returning objects.
      //Usage of lifecycle methods right now to produce data whenever the app is launched.
      //Use created  when making HTTP reqs and fetchig initial data.
      showAddTask:false,
    }
  },


  name: 'App',
  components: {
    Header,
    Footer,
}
}
</script>

<style>
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
