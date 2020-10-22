<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="add_todo" />
    <Todos v-bind:todos="todos" v-on:del-todo="delete_todo" />
  </div>
</template>

<script>
import Todos from "./components/todos";
import Header from "./components/layout/header";
import AddTodo from "./components/add_todo";
import axios from 'axios'

export default {
  name: "App",
  components: {
    Header,
    Todos,
    AddTodo
  },

  data() {
    return {
      todos:[] 
      
    };
  },
  methods:{
    delete_todo(id){

      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(this.todos=this.todos.filter(todo => todo.id!==id))
      .catch(err=> console.log(err))

      

    },
    add_todo(new_todo){

      const { title,completed}=new_todo;
      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
      .then(res=>this.todos=[...this.todos,res.data])
      .catch(err=>console.log(err))

      

    }
  },
  created(){
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
      .then(res =>this.todos=res.data)
      .catch(err=>console.log(err));
    }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn{
  display: inline-block;
  border: none;
  background: #555;
  color:#fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover{
  background: #666;
}


</style>
