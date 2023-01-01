<template>
    <div class="container" :key="props.story.id">
        <div class="header">
            <span>{{ props.story.title }}</span>
            <i class="fa-solid fa-angle-down" :class="{rotate: isShow}" @click="showContent"></i>
        </div>
        <div class="content" :class="{show: isShow}">
            {{ props.story.content }}
        </div>
    </div>
</template>

<script setup lang="ts">
    import { ref } from 'vue';

    interface Props {
        story: {
            id: number,
            title: string,
            content: string
        }
    }

    const props = defineProps<Props>();

    const isShow = ref(false);

    function showContent() {
        isShow.value = !isShow.value
    }
</script>

<style scoped>
.header {
    background-color: #385059;
    width: 100%;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 15px;
    font-size: 16px;
    font-weight: 600;
    color: #fff;
}

.header span, .header i {
    background-color: #385059;
}

i {
    font-size: 18px;
    cursor: pointer;
    transition: all 0.3s ease-in-out;
}

.content {
    width: 100%;
    background-color: #fff;
    height: 0;
    transform: scaleY(0);
    transform-origin: top;
    transition: transform 0.3s ease-in-out;
    overflow: hidden;
}

.show {
    height: auto;
    padding: 15px;
    transform: scaleY(1);
    box-shadow: 0px 10px 15px -3px rgba(0,0,0,0.1);
}

.rotate {
    transform: rotate(-180deg);
}

.container {
    width: 500px;
    border-radius: 5px;
    overflow: hidden;
}

</style>