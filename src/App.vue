<template>
<div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
</div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';
import axios from 'axios';

export default {
    name: 'app',
    components: {
        Header,
        Todos,
        AddTodo
    },
    data() {
        return {
            todos: []
        }
    },
    methods: {
        deleteTodo(id) {
            axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                .then(this.todos = this.todos.filter(todo => todo.id !== id))
                .catch(err => console.log(err))

        },
        addTodo(newTodo) {
            this.todos = [...this.todos, newTodo];
        }
    },
    created() {
        axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
            .then(res => this.todos = res.data)
            .catch(err => console.log(err))
    },
    mounted() {
        setTimeout(() => {
            let todoItems = document.querySelectorAll('.todo-item');
            todoItems.forEach(function (todoItem) {
                if (todoItem.className.indexOf("is-complete") >= 0) {
                    todoItem.querySelector('input[type=checkbox]').checked = true;
                }
            });
        }, 400);
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Manrope&display=swap');

body {
    background-color: #E1E1E1;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    color: var(--text-color);
    font-family: 'Manrope', sans-serif !important;
}

@media only screen and (max-width: 600px) {
    #app {
        width: 90% !important;
    }
}

#app {
    width: 35%;
    margin: auto;
    box-shadow: 0px 10px 20px 15px rgba(10, 10, 10, 0.25);
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: 'Open Sans', sans-serif;
    line-height: 1.4;
    background: rgb(30, 0, 36);
    background: linear-gradient(to right,rgb(115, 210, 144), rgb(105, 113, 156));
}
</style>
