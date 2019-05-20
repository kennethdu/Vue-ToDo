<template>
  <div id="task-form">
    <form @submit.prevent="handleSubmit">
      <label>Task Name</label>
      <input
        ref="first"
        type="text"
        :class="{ 'has-error': submitting && invalidTask }"
        v-model="task.name"
        @focus="clearStatus"
        @keypress="clearStatus"
      >
      <label>Task Description</label>
      <input
        type="text"
        :class="{ 'has-error': submitting && invalidDescription }"
        v-model="task.description"
        @focus="clearStatus"
      >
      <p v-if="error && submitting" class="error-message">❗Please fill out all required fields</p>
      <p v-if="success" class="success-message">✅ task successfully added</p>
      <button>Add task</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "to-do-form",
  data() {
    return {
      error: false,
      submitting: false,
      success: false,
      task: {
        name: "",
        description: ""
      }
    };
  },
  computed: {
    invalidTask() {
      return this.task.name === "";
    },
    invalidDescription() {
      return this.task.description === "";
    }
  },
  methods: {
    handleSubmit() {
      this.clearStatus();
      this.submitting = true;

      if (this.invalidTask || this.invalidDescription) {
        this.error = true;
        return;
      }

      this.$emit("add:task", this.task);
      this.$refs.first.focus();
      this.task = {
        name: "",
        description: ""
      };
      this.success = true;
      this.error = false;
      this.submitting = false;
    },
    clearStatus() {
      this.success = false;
      this.error = false;
    }
  }
};
</script>

<style lang="css" scoped>
form {
  margin-bottom: 2rem;
}

[class*="-message"] {
  font-weight: 500;
}

.error-message {
  color: #d33c40;
}

.success-message {
  color: #32a95d;
}
</style>