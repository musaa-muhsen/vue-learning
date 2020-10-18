<template>
    <div class="todo-item" v-bind:class="{'is-complete':todoProp.completed}">
       <p  > 
           <input type="checkbox" v-on:change="markComplete">
           {{todoProp.title}}
           <button v-on:click="$emit('del-todo', todoProp.id)" class="del">x</button>
           </p>
    </div>
<!--
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
         conditional above were binding the class if todo.completed is true, is completed will be added notice there is a static class as well v-bind:class="{'classname':condition true or false ternary operator }"   
        <p>
            {{todoProp.title}}
        </p>
    </div>
    -->
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todoProp"],
    methods: {
        markComplete() {
            console.log(this)
            // this is refering to this whole component 
        this.todoProp.completed = !this.todoProp.completed
    }

    } 
}
</script>





<style scoped>
   .todo-item {
       background: #f4f4f4;
       padding: 10px;
       border-bottom: 1px #ccc dotted;
   }
/*
            <input type="checkbox" v-on:change="markComplete" >

now i only want the line through if it's completed so in todo-item div basically we're gonna add kind of a conditional we're gonna bind the class on a condition of it's completed then we want to add the is complete class 
*/
   .is-complete {
       text-decoration: line-through;
   }

   .del {
       background: #ff0000;
       color: #fff;
       border: none; 
       padding: 5px 9px;
      /* border-radius: 50%;*/
       cursor: pointer;
       float: right;
   }
</style>