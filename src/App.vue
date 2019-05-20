<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <ToDoForm/>
    <ToDoTable/>
  </div>
</template>

<script>
import ToDoTable from "./components/ToDoTable";
import ToDoForm from "./components/ToDoForm";

export default {
  name: "app",
  components: {
    ToDoTable,
    ToDoForm
  },
  data(){
    return{
      tasks: []
    }
  },

  mounted(){
    // this.getTasks()
  },

  method: {
    // async getTasks(){

    // },
    // async addTask(task){

    // },
    // async editTask(id, updatedTask){

    // },
    // async deleteTask(id){

    // }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
