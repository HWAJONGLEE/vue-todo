<template>
  <div>
      <input type="text" v-model="newTodoItem">
  </div>
</template>

<script>
export default {
    data (){
        return{
            newTodoItem: "",
        }
    },
    methods : {
        addTodo (){
            console.log(this.newTodoItem);
            this.newTodoItem='';
        }
    }
}
</script>

<style>

</style>