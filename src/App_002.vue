<script setup>
import { ref} from 'vue'

const todolist = ref([{
        description: 'Posprzątać pokój',
        done: false,
        id: 1
    } , {
        description: 'Pouczyć się !',
        done:false,
        id: 2
    }]

)

 function addTodo(e) {
    e.preventDefault()
    console.log(e)
    todolist.value.push({
        description: 'kolejna rzecz do zrobienia',
        done:false,
        id: todolist.value.length + 1
    });
}

    function taskDone(todo) {
        todo.done = !todo.done
    }
//  function test() {
// console.log('test')
//  }
</script>

<template>
<p> lista zadań:</p>
<ul>
    <li v-for="todo in todolist" 
    :key="todo.id" 
    @click.stop="taskDone(todo)" 
    class="todo" 
    :class="{'todo-done': todo.done}">
{{ todo.id }}, {{ todo.description }}
    </li>
</ul>
<!-- <button @click="addTodo" >Dodaj zadanie</button> -->
<a href="https://www.google.com" @click.prevent="addTodo">Dodaj zadanie</a>

</template>

<style>
.todo {
    font-weight: bold;
}
.todo-done {
    text-decoration: line-through;
}
</style>