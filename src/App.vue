<template>
  <div id="app">
    <img weight=100px height=100px src="./assets/hiyouth_logo.png">
    <h1>welcome {{ msg }}</h1>
    <input type="text" v-model="todo" @keydown="addList($event)"/>
    <!-- <button v-on:click="addList()">ADD+</button> having using keyboard-->
    <br>
    <hr>
    <section>
    <h2>PENDING </h2>
    <ol v-for="(item,key) in list" v-if="!item.checked">
    <li>
    <input type="checkbox" v-model="item.checked" @change="saveChange()"/>{{item.text}}--{{key}}
    <button v-on:click="deleteData(key)" >delete</button>
    </li>
    </ol>
    </section>
    <section class="comp_bg">
    <h2> COMPLETING </h2>
    <ol v-for="(item,key) in list" v-if="item.checked">
    <li>
    <input type="checkbox" v-model="item.checked"/>{{item.text}}--{{key}}
    <button v-on:click="deleteData(key)" >delete</button>
    </li>
    </ol>
    </section>
  </div>
</template>

<script>
import storage from './model/storage.js'
export default {
  name: 'app',
  data () {
    return {
      todo:'',
      msg: 'HiYouth',
      obj: {
        name:"Alexa"
      },
      list: JSON.parse(storage.get('list')),
    }
  },
  methods:{
    getMsg(){
      alert(this.msg);
    },
    addList(e){ 
      if(e.keyCode === 13){  
        this.list.push({
          text:this.todo,
          checked:false,
        }); 
        this.todo = '';
      }  
      storage.set('list', JSON.stringify(this.list))    
    },
    deleteData(key){       
        this.list.splice(key,1);
        storage.set('list', JSON.stringify(this.list))   
    },
    saveChange(){
        storage.set('list', JSON.stringify(this.list))
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.comp_bg {
  background-color: #42b983;
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 auto;
}

a {
  color: #42b983;
}
</style>
