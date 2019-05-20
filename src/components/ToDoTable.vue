<template>
  <div id="task-table">
    <p v-if="tasks.length < 1" class="empty-table">No tasks</p>
    <table class="table is-fullwidth" v-else>
      <thead>
        <tr>
          <th>Name</th>
          <th>Task Description</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr :key="task.id" v-for="task in tasks">
          <td v-if="editing === task.id">
            <input type="text" v-model="task.name">
          </td>
          <td v-else>{{task.name}}</td>
          <td v-if="editing === task.id">
            <input type="text" v-model="task.description">
          </td>
          <td v-else>{{task.description}}</td>
          <td v-if="editing === task.id">
            <button class="button is-link" @click="editTask(task)">Save</button>
            <button class="muted-button button is-link" @click="editing = null">Cancel</button>
          </td>
          <td v-else>
            <button class="button is-link" @click="editMode(task.id)">Edit</button>
            <button class="button is-link" @click="$emit('delete:task', task.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "to-do-table",
  props: {
    tasks: Array
  },
  data() {
    return {
      editing: null
    };
  },
  methods: {
    editMode(id) {
      this.editing = id;
    },
    editTask(task) {
      if (task.name === "" || task.description === "") return

      this.$emit("edit:task", task.id, task);
      this.editing = null;
    }
  }
};
</script>

<style>
.button {
  margin: 1%;
}
.empty-table {
  text-align: center;
}
</style>