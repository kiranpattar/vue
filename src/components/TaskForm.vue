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
      <button v-if="id" @click="updateTask(id)">Update Task</button>
      <button v-else>Add Task</button>

    </div>
  </form>
</template>

<script>
export default {
  name: "TaskForm",
  props:{
    id:String
  },
  data() {
    return {
      formValues: {
        name: "",
        priority: "low",
        editClick:false
      },
    };
  },
  methods: {
    submitForm() {
      this.$emit("submitTask", { ...this.formValues });
      this.formValues.name = "";
    },
    updateTask(id){
      console.log(id,this.formValues)
      this.$emit("updateTask", id,this.formValues);
    }
  },
};
</script>

<style scoped>
/*  */
</style>
