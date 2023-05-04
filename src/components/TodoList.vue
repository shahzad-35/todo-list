<template>
    <h1>Todo List</h1>
    <div class="list">
        <input type="text" placeholder="Enter Task...." v-model="task">
        <button @click="saveTask">Save</button>
        <h3>-------------------------------------</h3>
        <ul v-for="(todo, index) in todos" :key="index">
            <li :class="{done:todo.done}" @click="markDone(todo)">
                {{ todo.text }}
            </li>
        </ul>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    name: 'TodoList',
    data() {
        return {
            task: '',
            todos: []
        }
    },
    mounted() {
        let todosData = JSON.parse(localStorage.getItem('todos')) || this.todos;
        this.todos = ref(todosData)
    },
    methods: {
        saveTask() {
            if (this.task !== "") {
                this.todos.push({
                    text: this.task,
                    done: false
                })
                this.task = ""
                this.setStorage();
            }
        },
        markDone(todo) {
            todo.done = !todo.done;
            this.setStorage();
            console.log(this.todos);
        },
        setStorage() {
            const storageData = JSON.stringify(this.todos);
            localStorage.setItem('todos', storageData);
        }
    }
}
</script>

<style scoped>
h1 {
    color: rgb(33, 39, 39);
}

.list {
    width: 550px;
    margin: 0 auto;
    height: 525px;
    background: linear-gradient(to bottom right, #d6e1e4, #85c5d4);
    background-repeat: no-repeat;
    background-attachment: fixed;
    border-radius: 10px;
}

input {
    width: 75%;
    height: 35px;
    box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.18);
    border-radius: 5px;
    border: 1px solid #cbcbcb;
    padding-left: 9px;
    font-size: 1.05rem;
    margin: 15px 5px 0px 5px;
}

button {
    margin-left: 5px;
    width: 14%;
    cursor: pointer;
    height: 7%;
    border-radius: 4px;
    background-color: rgb(37, 199, 51);
    color: rgb(24, 22, 22);
    font-size: 1rem;
    width: 10%;
}

h3 {
    margin-top: 25px;
}

li {
    min-width: 92%;
    width: fit-content;
    background-color: rgb(220 222 218);
    padding-left: 7px;
    padding-top: 10px;
    cursor: pointer;
    padding-bottom: 6px;
    font-size: 1.2rem;
    text-align: left;
    margin-bottom: 5px;
    margin-left: 15px;
    height: 25px;
    border-radius: 5px;
}

.done {
    text-decoration: line-through;
}
</style>