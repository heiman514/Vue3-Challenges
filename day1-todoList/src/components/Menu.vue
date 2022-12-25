<script setup lang="ts">
    import {ref} from 'vue';

    let page = ref(props.page);

    const props = defineProps<{
        page: String, 
        changeComponent: Function
    }>()

    function handlePageToggle(newPage) {
        props.changeComponent(newPage);
        page.value = newPage;
    }
</script>

<template>
    <div class="Menu">
        <h3>Menu</h3>
        <button id="today" @click="handlePageToggle($event.currentTarget.id)">
            <i class="fa-solid fa-calendar-day" :class="{active: page === 'today'}"></i>
            <span>Today's Todos</span>
        </button>
        <button id="scheduled" @click="handlePageToggle($event.currentTarget.id)">
            <i class="fa-solid fa-calendar-days" :class="{active: page === 'scheduled'}"></i>
            <span>Scheduled Todos</span>
        </button>
        <button id="completed" @click="handlePageToggle($event.currentTarget.id)">
            <i class="fa-regular fa-circle-check" :class="{active: page === 'completed'}"></i>
            <span>Completed Todos</span>
        </button>
    </div>
</template>

<style scoped>
    .Menu {
        width: 25%;
        height: 100%;
        padding: 3.5rem 0;
        background-color: #FFF;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    h3 {
        color: #333;
    }

    button {
        width: 90%;
        height: 3rem;
        border-radius: 0;
        background-color: #FFF;
        display: flex;
        align-items: center;
        gap: 1rem;
        transition: all 0.2s;
        margin: 0.3rem 0;
        color: #444;
    }

    i {
        color: #999;
    }

    i.active {
        color: #C98CFE;
    }

    button:hover i {
        color: #fff;
    }

    button:hover {
        background-color: #A18AFF;
        color: #fff;
    }
    
</style>