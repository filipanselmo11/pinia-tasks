<template>
    <form @submit.prevent="handleSubmit">
        <input placeholder="I need to..." type="text" v-model="newTask">
        <button @click="handleSubmit()">Add</button>
    </form>
</template>

<script>
import { useTaskStore } from '@/stores/TaskStore';
import { ref } from 'vue';

export default {
    setup() {
        const taskStore = useTaskStore();
        const newTask = ref('');
        const handleSubmit = () => {
            if (newTask.value.length > 0) {
                taskStore.addTask({
                    title: newTask.value,
                    isFav: false,
                    id: Math.floor(Math.random() * 10000)
                })
                newTask.value = ''
            }
        }

        return { newTask, handleSubmit }
    }
}
</script>