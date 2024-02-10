<template>
    <div class="flex flex-col items-center mt-10">
        <h1 class="text-3xl">Inertia Task Manager</h1>
        <form @submit.prevent="submit">
            <div class="mt-5 flex flex-col items-center">
                <input type="text" id="input" v-model="newTask.description" placeholder="New Task..."
                    class="p-2 rounded shadow" style="text-indent: 10px; min-width: 400px">
                <button class="rounded-full bg-blue-400 py-3 px-5 mt-4 max-w-fit" type="submit">Add Task</button>
            </div>
        </form>

        <ul class="list-unstyled mt-10">
            <template v-for="task in tasks" :key="task.id">
                <li class="p-8 my-3 border flex justify-between align-center" style="min-width: 400px;">
                    <span>{{ task . description }}</span>
                    <form @submit.prevent="deleteTask(task.id)">
                        <button class="bg-red-500 hover:bg-red-600 text-white font-bold py-1 px-4 rounded focus:outline-none focus:shadow-outline-red active:bg-red-800" type="submit">X</button>
                    </form>
                </li>
            </template>
        </ul>
    </div>
</template>

<script setup>
    import {
        reactive,
    } from 'vue';

    import {
        router
    } from '@inertiajs/vue3';

    const props = defineProps({
        tasks: Array
    })

    const newTask = reactive({
        description: null,
        is_completed: false
    });


    const submit = () => {
        router.post('/tasks', newTask);
        newTask.description = '';
    }

    const deleteTask = (id) => {
        router.delete(`/tasks/${id}`, {
            onBefore: () => confirm('Are you sure?')
        });
    }
</script>

<style lang="scss" scoped>

</style>
