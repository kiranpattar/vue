<template>
  <div>
    <div id='header'>
        <h2>Priority To-Do List</h2>
        <h2 v-if="saveData">Saved Successfully</h2>
    </div>
    <!-- Form Component -->
    <TaskForm
    @submitTask="submitForm"
    />

    <!-- List Component -->
    <TaskList
      :tasks="listValues"
      @editTask="editRow"
      @deleteTask="deleteRow"
     @updateTask="updateTask"
    />

    <div v-if="listValues.length > 0" id="updateData">
      <button @click="onSave">Save</button>
      <button @click="deleteEntireTable">Clear</button>
    </div>
  </div>
</template>

<script>
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";

export default {
  name: "App",
  components: {
    TaskForm,
    TaskList,
  },
  data() {
    let savedTasks = JSON.parse(localStorage.getItem("taskLists")) || [];
    return {
      listValues: savedTasks,
      saveData:false,
    };
  },
  methods: {
    updateTask(index,formValues){
      console.log(index,formValues)
        if(formValues.name !== "")
        this.listValues[index] = formValues
        else
        alert("Please enter valid string")
    },
    submitForm(task) {
      console.log(task,"submitForm")
      if (task.name === "") {
        alert("Name is empty");
        return;
      }
      this.listValues.push({
        ...task,
        id: this.listValues.length,
      });
    },
    editRow(index) {
      this.listValues[index].editClick = !this.listValues[index].editClick
      console.log("Edit row:", index);
    },
    deleteRow(index) {
      this.listValues.splice(index, 1);
    },
    deleteEntireTable() {
      if (confirm("Are you sure you want to delete all tasks?")) {
        this.listValues = [];
        localStorage.removeItem("taskLists");
      }
    },
    onSave() {
      localStorage.setItem("taskLists", JSON.stringify(this.listValues));
      this.saveData = true;
      let timer = setTimeout(()=>{
        this.saveData = false
        clearTimeout(timer)
      },2000)
    },
  },
};
</script>

<style>
#formField {
  display: grid; 
    grid-template-columns: 2fr 1fr auto;
    grid-gap: 10px;
    padding: 5px;
    /* border: 1px solid green; */
    align-items: center;
    border-bottom: 1px dashed green;
    align-content: stretch;
    justify-content: space-evenly;
}

#formField input,  select {
  width: 40%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

 button {
  padding: 8px 16px;
  background-color: green;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 4px;
}

#formField button:hover,#listItems button:hover {
  background-color: darkgreen;
}

#formField,
#updateData {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  gap: 10px;
  margin:20px 0px;
}
h2:nth-child(2) {
  color: green;

  
}
#header {
  display:flex;
  border-bottom:1px dashed green;
  justify-content:space-between;

}
#header h2 {
   margin:10px 0 0 10px;
}

</style>
