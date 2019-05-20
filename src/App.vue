<template>
  <div id="app" class="container">
    <Header/>
    <ToDoForm @add:task="addTask"/>
    <ToDoTable :tasks="tasks" @delete:task="deleteTask" @edit:task="editTask"/>
  </div>
</template>

<script>
import Header from './components/Header'
import ToDoTable from "./components/ToDoTable";
import ToDoForm from "./components/ToDoForm";

export default {
  name: "app",
  components: {
    Header,
    ToDoTable,
    ToDoForm
  },
  data() {
    return {
      tasks: []
    };
  },

  mounted() {
    this.getTasks();
  },

  methods: {
    async getTasks() {
      try {
        const response = await fetch(
          "https://my-json-server.typicode.com/kennethdu/to-do-vue-json/tasks"
        );
        const data = await response.json();
        this.tasks = data;
      } catch (error) {
        console.error(error);
      }
    },
    async addTask(task) {
      try {
        const response = await fetch(
          "https://my-json-server.typicode.com/kennethdu/to-do-vue-json/tasks",
          {
            method: "POST",
            body: JSON.stringify(task),
            headers: {
              "Content-type": "application/json; charset=UTF-8"
            }
          }
        );
        const data = await response.json();
        this.tasks = [...this.tasks, data];
      } catch (error) {
        console.error(error);
      }
    },
    async editTask(id, updatedTask) {
      try {
        const response = await fetch(
          `https://my-json-server.typicode.com/kennethdu/to-do-vue-json/tasks/${id}`,
          {
            method: "PUT",
            body: JSON.stringify(updatedTask),
            headers: {
              "Content-type": "application/json; charset=UTF-8"
            }
          }
        );
        const data = await response.json();
        this.tasks = this.tasks.map(tasks => (tasks.id === id ? data : tasks));
      } catch (error) {
        console.error(error);
      }
    },
    async deleteTask(id) {
      try {
        await fetch(
          `https://my-json-server.typicode.com/kennethdu/to-do-vue-json/tasks/${id}`,
          {
            method: "DELETE"
          }
        );
        this.tasks = this.tasks.filter(tasks => tasks.id !== id);
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>

<style>
#app {
  text-align: center;
}
</style>
