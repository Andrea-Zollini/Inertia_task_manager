<template>
    <div class="flex flex-col items-center mt-10">
        <h1 class="text-3xl">Inertia Task Manager</h1>
        <div class="mt-5 flex flex-col items-center">
            <input type="text" v-model="newTask" placeholder="New Task..." class="p-2 rounded shadow"
                style="text-indent: 10px;">
            <button class="rounded-full bg-blue-400 py-3 px-5 mt-4 max-w-fit" @click="addTask()">Add Task</button>
        </div>
    </div>
</template>

<script setup>
    import { ref } from 'vue';

    const newTask = ref(null);

    const addTask = () => {
        console.log(newTask.value);
    }
</script>

<style lang="scss" scoped>

</style>
