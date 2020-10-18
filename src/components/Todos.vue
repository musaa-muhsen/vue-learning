<template>
    <div class="todos-container">
        
            <!-- <h3>{{todo.title}}</h3> -->
            <TodoItem class="looped" v-on:del-todo="$emit('del-todo', todo.id)" v-bind:key="todo.id" v-for="todo in todosProp" v-bind:todoProp="todo"/>
            <!-- prop drilling ^^^ -->
        
    </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

    // name will be the component name when exported 
export default {
    name: "TodosComp",
    components: {
       TodoItem
    },
    props: ["todosProp"]
}
// We can use the v-on directive to listen to DOM events and run some JavaScript when they’re triggered.
  

</script>

<style scoped>

</style>