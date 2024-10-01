<template>
    <div>
                <h2>Priority To-Do List</h2>
            </div>
    <form @submit.prevent="submitForm">
        <div id="formField">
            <div>
                <input @keyup.enter="submitForm" id="name" placeholder="Name" v-model.trim.lazy="formValues.name"  type="text"/>
            </div>
            <div>
                <select  @keyup.enter="submitForm" name="priority"  v-model="formValues.dropValue" id="priority">
                  <option value="critical">Critical</option>
                  <option value="moderate">Moderate</option>
                  <option value="low">Low</option>
                </select>
            </div>
            <button >Add to-do-list </button>
        </div>
    </form>
        <div >
            <ul>
              <li v-for="(obj,index) in listValues" :key="obj.name">
                 <div id="listItems">
                    <div> 
                      <div v-if= "obj.editRowData == false"> {{obj.name}}</div>
                      <!-- <input type=text v-if= "obj.editRowData == true" v-model="obj.name"/>  -->
                    </div>
                    <div> 
                      {{obj.dropValue}} 
                    </div>
                    <button @click="editRow" :id="index" key="" >
                      Edit 
                    </button>
                    <button @click="deleteRow" :id="index" key="" >
                      Delete 
                    </button>
                 </div>
              </li>   
            </ul>
        </div>

        <div v-if="listValues.length > 0" id="updateData">
            <div>
                <button @click="onSave">Save </button>
            </div>
            <div>
                <button @click="deleteEntireTable" >Clear </button>
            </div> 
        </div>
     </template>   


<script>

export default {
  name: 'App',
  data(){
    if(window.localStorage.getItem('taskLists') !== "")
    this.taskLists = JSON.parse(window.localStorage.getItem('taskLists'))
    else 
    this.taskLists = []
    return {
      formValues:{
        name:'',
        dropValue:'low',
        delete1:'',
        editRowData:false,
      },
      listValues: this.taskLists.length>0?this.taskLists:[]
    }    
  },
methods:{
  editRow(evt){
    console.log(evt.target.id)
    // this.listValues[index].editRowData=true
  },
  submitForm(evt){
    // event.preventDefault()
    // console.log('form values',this.formValues)
    // const {delete1} = this.formValues;
    if(this.formValues.name == ""){
      alert("Name is empty")
      evt.preventDefault()  
      return false

    }
    this.listValues.push({
      ...this.formValues,
      delete1 : this.listValues.length
    })
    this.formValues.name = ""
    console.log(this.listValues,"listValues")

  },
  deleteRow(evt){
      console.log(evt.target.id,"id")
      // if(this.listValues.length > -1)
      this.listValues.splice(evt.target.id,1)
  },
  deleteEntireTable(){
    let text = "Are you sure you want to delete the table";
        if (confirm(text) == true) {
          this.listValues = []
          window.localStorage.setItem('taskLists', '');
        } else {
          return false
        }
  },
  onSave(){
    window.localStorage.setItem('taskLists', JSON.stringify(this.listValues));
  },
  mounted(){
    this.taskLists = JSON.parse(localStorage.get('taskLists'));
    console.log(this.taskLists)
  }
}
}
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50; */
}
ul {
  background: white;
  list-style: none;
}
ul li {
  background: white;
  color: black;
  padding: 5px;
  border:1px solid orange;

}

#listItems {
  display: flex;
    width: 100%;
    flex-direction: row;
    flex-wrap: wrap;
    align-content: stretch;
    align-items: baseline;
    justify-content: space-evenly;
}
#listItems div {
  width : 35%;

}
#formField ,#updateData{
  display: flex; /* or inline-flex */
  border: 1px solid green;
  justify-content: space-between;
    align-items: flex-start;
    flex-wrap: nowrap;
    flex-direction: row;
    padding:10px
}


</style>
