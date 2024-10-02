<template>
  <div>
    <ul>
      <li v-for="(task, index) in tasks"  :key="task.name">
        <div  id="listItems">
          <div>{{ task.name }}</div>
          <div>{{ task.priority }}</div>
          <button @click="toggleEdit(index)">Edit</button>
          <button @click="deleteTask(index)">Delete</button>
        </div>
        <TaskForm      
        @updateTask="updateTask"
        v-if="task.editClick" 
        :id = "index" 
        @submitTask="submitForm" />
      </li>
    </ul>
  </div>
</template>

<script>
import TaskForm from "../components/TaskForm.vue";

export default {
  name: "TaskList",
  components: {
    TaskForm,
  },
  props: {
    tasks: Array,
  },
  methods: {
    data(){
      return {
        // formValues: {
        // name: "",
        // priority: "low",
        // },
        editSet:false
      }
    },
    editTask(index) {
      this.$emit("editTask", index);
    },
    toggleEdit(index) {
      console.log("lol",this.editSet)
      this.$emit("editTask", index,);
      // console.log(tasks,"tasks")
      // this.editSet = !this.editSet
    },
    deleteTask(index) {
      this.$emit("deleteTask", index);
    },
    updateTask(index,formValues){
      console.log(index)
      this.$emit("updateTask",index,formValues)
        // this.listValues[index] = formValues
    },
  },
};
</script>

<style scoped>
ul {
  background: white;
  list-style: none;
  padding: 0;
  margin: 0;
}

ul li {
  display: grid;
  grid-template-columns: 2fr 1fr 0.5fr 0.5fr;
  background: white;
  color: black;
  padding: 10px;
  border: 1px solid orange;
  align-items: center;
  gap: 10px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  border-radius: 8px; 
  border: 1px solid #e0e0e0; 
}

#listItems {
  display: contents; 
}

#listItems div {
  padding: 10px;
}

button {
  padding: 5px 10px;
  background-color: orange;
  border: none;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: darkorange;
}

 li #formField, #updateData {
    display: flex;
    justify-content: space-between;
    padding: 10px;
    gap: 10px;
    margin: 20px 0px;
    width:100%
}
</style>
