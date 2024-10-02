<template>
  <form @submit.prevent="submitForm">
    <div id="formField">
      <input
        @keyup.enter="submitForm"
        id="name"
        placeholder="Name"
        v-model.trim.lazy="formValues.name"
        type="text"
      />
      <select v-model="formValues.priority">
        <option value="critical">Critical</option>
        <option value="moderate">Moderate</option>
        <option value="low">Low</option>
      </select>
      <button>Add Task</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "TaskForm",
  data() {
    return {
      formValues: {
        name: "",
        priority: "low",
      },
    };
  },
  methods: {
    submitForm() {
      this.$emit("submitTask", { ...this.formValues });
      this.formValues.name = "";
    },
  },
};
</script>

<style scoped>
/*  */
</style>
