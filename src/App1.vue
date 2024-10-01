<template>
 <div>
    {{greet}} {{name}}
  </div>
  <div v-html="channel"></div>
   <div v-text="channel"></div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data(){
    return {
      greet:"Helo1",
      name:"Kiran Pattar1",
      channel:'<b>kiran</b>'
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>


<template>
 <h2 v-if = "num === 0"> Num is zero </h2>
<!-- <h2 v-if = "num === 1"> Num is 1 </h2>
 <h2 v-else> Num is 15 </h2> -->
 <h2 v-for="(name,index) in names" :key="name"> {{name}} {{index}}</h2>
  <template v-for="(name,index) in fullNames" :key="name.first"> {{name.first}} 
     {{name.last}}{{index}}
     <input placeholder="Last Name" /> 
     </template>
  <button @click="shuffle"> Add</button>

</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data(){
    // return {
    //  num:15
    // }
    return {
        names:['bruce','clark','Diana'],
        fullNames:[
            {first:'kiran',last:'pattar'},
             {first:'abc',last:'def'},
              {first:'ijk',last:'lmn'},
               {first:'hij',last:'klm'}
        ]
    }
  },
methods:{
    shuffle(    ){
        this.fullNames.push({first:'kiran',last:'pattar'})
    }
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
