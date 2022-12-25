<script setup lang="ts">
    import { ref, reactive, computed } from 'vue';
    import TodoItem from './TodoItem.vue'
    defineProps<{ title: String, page: String }>()
    
    const newTodo = ref('');

    const date = new Date();
    let day = date.getDate();
    let month = date.getMonth() + 1;
    let year = date.getFullYear();
    let currentDate = `${year}-${month}-${day}`;
    const dateDisplay = ref(currentDate);
    const timeDisplay = ref(date.toLocaleTimeString('it-IT').substring(0,5));

    let todos = reactive(JSON.parse(localStorage.getItem('todos')) || []);

    function save() {
        localStorage.setItem('todos', JSON.stringify(todos));
    }

    function handleSubmit() {        
        if(newTodo.value) {        
            todos.push({
                content: newTodo.value,
                isCompleted: false,
                date: dateDisplay.value,
                time: timeDisplay.value
            });
            save();
            newTodo.value = '';
        }
    }

    function handleComplete(todo) {    
        todo.isCompleted = !todo.isCompleted;
        save();
    }

    function handleDelete(todoIndex) {
        todos.splice(todoIndex, 1);
        save();
    }

</script>

<template>
    <div class="todoList">
        <h3>{{title}}</h3>
        <div class="inputContainer">
            <input placeholder="What is your next task?" type="text" v-model="newTodo" v-on:keyup.enter="handleSubmit"/>
            <div class="dateTime">
                <input type="time" v-model="timeDisplay"/>
                <input type="date" v-model="dateDisplay"/>
            </div>
        </div>
        <div>
            <TodoItem 
                v-for="(todo, index) in todos"
                :key="index"
                :index="index"
                :todo="todo"
                :page="page"
                :currentDate="currentDate"
                :handleComplete="handleComplete"
                :handleDelete="handleDelete"
            />
        </div>
    </div>
</template>

<style scoped>
    h3 {
        text-align: start;
        font-size: 1.5rem;
        font-weight: 600;
    }

    .todoList {
        width: 75%;
        background-color: #A18AFF;
        padding: 3rem;
    }

    .inputContainer {
        height: 3rem;
        background-color: #fff;
        border-radius: 1rem;
        box-shadow: 0 0 5px rgba(0,0,0,0.2);
        display: flex;
        padding: 0 1rem;
    }

    input {
        outline: none;
        border: none;
    }

    input[type="text"] {
        width:60%;
        padding: 1rem;
        font-size: 14px;
    }

    .dateTime {
        font-size: 1.1rem;
        min-width: 4rem;
        width: 40%;
        display: flex;
        align-items: center;
        justify-content: space-around;
        color: #C98CFE;
    }

    .dateTime input {
        cursor: pointer;
        color: #333;
    }
</style>