<template>
    <div :key="task.id" v-for="task in tasks">
        <Task_View @toggle-reminder="$emit('toggle-reminder', task.id)" @delete-task="$emit('delete-task', task.id)"
            :task="task" />
    </div>
</template>

<script>
import Task_View from './Task_View.vue';


export default {
    name: "Tasks_View",
    props: {
        tasks: Array,
    },
    components: { Task_View },
    emits: ['delete-task', 'toggle-reminder']
}

</script>