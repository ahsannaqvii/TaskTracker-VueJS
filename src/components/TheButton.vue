<template>
 <button  v-on:click="onClick()"   v-bind:style={background:color} class="btn">
    <h1>{{text}}</h1>
 </button>
</template>

<script>
export default {
  methods: {
    onClick(){
      
        console.log('click')
        this.$emit('btn-click')
    }
  },
  props: {
    text:String,
    color:String,
  },
  name: 'TheButton',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped> 

</style>
