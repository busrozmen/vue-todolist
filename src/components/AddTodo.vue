<template>
<div class="addtodo">
    <form @submit="addTodo">
        <input type="text" v-model="title" name="title" placeholder="Add Todo">
        <input type="submit" value="+" class="">
    </form>
</div>
</template>

<script>
export default {
    name: "AddTodo",
    data() {
        return {
            title: '',
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault();
            const newTodo = {
                id: Math.floor(Math.random() * 10000),
                title: this.title,
                completed: false
            }
            this.$emit('add-todo', newTodo);
        }
    }
}
</script>

<style scoped>
.addtodo {
    margin: auto;
}

form {
    display: flex;
}

input[type="text"] {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
    font-family: 'Open Sans', sans-serif;
    line-height: 1.4;
}

input[type="submit"] {
    background-color: #2b3069;
    border: none;
    color: white;
    text-align: center;
    padding: 12px 20px;
    margin: 8px 0;
    font-size: 20px;
}
</style>
