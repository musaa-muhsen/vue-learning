<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" name="name-title" placeholder="Add Todo...">
            <input type="submit" value="Submit" class="btn"> 
        </form>
    </div> 
</template>

<script>
//import { v4 as uuidv4 } from 'uuid';


export default {
    name: "AddTodoComp",
    data() {
        return {
            title: ''
        }
    }, 
    methods: {
        addTodo(e) {
            e.preventDefault(); 

            const newTodo = {
                //id: uuidv4(),
                title: this.title,
                completed: false
                // this as in the whole component 
            }
    // this is going to traverse up this is taken from @submit="AddTodoComp" and were not using emmit
    // send up to parent by emmit an event, the emit is going to contain the newTodo object 
    this.$emit('add-todo', newTodo);
    
    this.title = '';

        }
    }
}
</script>







<style scoped>
 form {
     display: flex;
 }

 input[type="text"] {
     flex: 6;
     padding: 5px;
 }
 input[type="submit"] {
     flex: 2;
 }
</style>