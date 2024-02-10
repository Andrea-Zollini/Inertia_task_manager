<template>
    <div class="flex flex-col items-center mt-10">
        <h1 class="text-3xl">Inertia Task Manager</h1>
        <form @submit.prevent="submit">
            <div class="mt-5 flex flex-col items-center">
                <input type="text" id="input" v-model="newTask.description" placeholder="New Task..." class="p-2 rounded shadow"
                    style="text-indent: 10px; min-width: 400px">
                <button class="rounded-full bg-blue-400 py-3 px-5 mt-4 max-w-fit" type="submit">Add Task</button>
            </div>
        </form>

        <ul class="list-unstyled mt-10">
            <template v-for="task in tasks" :key="task.id">
                <li class="p-8 my-3 border" style="min-width: 400px;">{{ task.description }}</li>
            </template>
        </ul>
    </div>
</template>

<script setup>
    import {
        reactive,
        onMounted
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

    onMounted(() => {
        console.log(props.tasks);
    })
</script>

<style lang="scss" scoped>

</style>
