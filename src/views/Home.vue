<template>

  <div id="app">
    <Header />
    <AddTodoComp v-on:add-todo="addTodo" />
<!-- above is obtained from the emmit from addtodocomp  -->
<TodosComp v-bind:todosProp="todosObj" v-on:del-todo="deleteTodo"/>  
<!-- del-todo is where the id comes from  -->


<!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
<!-- pass in the data with directives called v-bind etc  
Directive - An order or instruction, especially one issued by an authority. The definition of directive is something related to management or control of an operation. ... A directive is defined as an order or an official instruction. When your boss orders you to call a client, this is an example of a directive.
-->
<!-- bind = put together, fasten, stick together -->
  </div>
</template>

<script>
import Header from '../components/layout/Header';
import TodosComp from '../components/Todos';
import AddTodoComp from '../components/AddTodoComp';
import axios from 'axios';

// is data like state??
// data is function and its going to return an object 
export default {
  name: 'Home',
  components: {
    Header,
    TodosComp,
    AddTodoComp
  },
  data() {
    return {
      todosObj: [
       
      ]
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then((response) => {
        console.log(response)
        // delete the id if it's true 
          this.todosObj = this.todosObj.filter(todo => todo.id !== id);        
      })
      .catch(err => console.log(err))
       // this will create a new data object todosObj      
    },
    addTodo(newTodo) {
      const {title, completed} = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title : title,
        completed : completed
      }).then(response => {
        console.log(response)
        this.todosObj = [...this.todosObj, response.data]
        }).catch(err => console.log(err))
          console.log(newTodo) 
  // json placeholder doesn't give us a database that persisits obviously they're not going to do that because people would just flood it but it does mimix a real back-end API the only different is it doesnt stick so if you reload it still goes away  
    } 
  },
  created() {
    // created is just like componentjustmount in react 
        axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
         .then(res => this.todosObj = res.data)
         .catch(err => console.log(err))
  }
}

</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family:  Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
 line-height: 1.4;
}
/* added to the main but used throughout the components */
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>

