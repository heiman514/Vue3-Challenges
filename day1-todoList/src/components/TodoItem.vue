<script setup lang="ts">
    import { watch, ref } from 'vue';
    interface Todo {
        content: String,
        isCompleted: Boolean,
        date: String,
        time: String
    }

    const props = defineProps<{ 
        todo: Todo,
        handleComplete: Function,
        index: Number,
        handleDelete: Function,
        currentDate: String,
        page: String
    }>()

    const isCompleted = ref(props.todo.isCompleted);

    function handleToggle() {
        props.handleComplete(props.todo);
        isCompleted.value = !isCompleted.value;
    }
</script>

<template>
    <div class="itemContainer" v-if="currentDate === todo.date && props.page === 'today'">
        <p>{{todo.content}}</p>
        <p>{{todo.time}}</p>
        <div class="itemBtn">
            <i class="fa-regular fa-circle" v-if="!isCompleted" @click="handleToggle"></i>
            <i class="fa-regular fa-circle-check" v-if="isCompleted" @click="handleToggle"></i>
            <i class="fa-solid fa-trash" @click="handleDelete(index)"></i>
        </div>
    </div>
    <div class="itemContainer" v-if="props.page === 'scheduled'">
        <p>{{todo.content}}</p>
        <p>{{todo.date}}</p>
        <div class="itemBtn">
            <i class="fa-regular fa-circle" v-if="!isCompleted" @click="handleToggle"></i>
            <i class="fa-regular fa-circle-check" v-if="isCompleted" @click="handleToggle"></i>
            <i class="fa-solid fa-trash" @click="handleDelete(index)"></i>
        </div>
    </div>
    <div class="itemContainer" v-if="props.page === 'completed' && todo.isCompleted">
        <p>{{todo.content}}</p>
        <p>{{todo.date}}</p>
        <div class="itemBtn">
            <i class="fa-regular fa-circle" v-if="!isCompleted" @click="handleToggle"></i>
            <i class="fa-regular fa-circle-check" v-if="isCompleted" @click="handleToggle"></i>
            <i class="fa-solid fa-trash" @click="handleDelete(index)"></i>
        </div>
    </div>
</template>

<style scoped>
    .itemContainer {
        height: 3rem;
        text-align: start;
        padding: 0 2rem;
        border-radius: 1rem;
        box-shadow: 0 0 5px rgba(0,0,0,0.2);
        background-color: #fff;
        display: flex;
        align-items: center;
        margin: 1rem 0;
    }
    
    p {
        color: #333;
    }

    p:nth-child(1) {
        width: 75%;
    }

    p:nth-child(2) {
        width: 15%;
        color: #555;
        font-size: 600;
        text-align: end;
        margin-right: 1rem;
    }

    i {
        font-size: 1.1rem;
        cursor: pointer;
    }

    .fa-circle {
        color: #DDD;
    }

    .fa-circle-check {
        color: #C98CFE;
    }

    .fa-trash {
        color: #ED5E68
    }

    .itemBtn {
        width: 10%;
        display:flex;
        gap: 1rem;
        justify-content: flex-end;
    }
</style>