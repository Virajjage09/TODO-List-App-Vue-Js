<template>
    <header>
        <h1>{{ title }}</h1>
        <Button v-show="homePage" @btn-click="$emit('toggle-add-task')" :text="showAddTask ? 'Close' : 'Add TODO'"
            :color="showAddTask ? 'grey' : 'blue'" />
    </header>
</template>

<script>

import Button from './Button_View.vue'

export default {
    name: 'Header_View',
    props: {
        title: String,
        showAddTask: Boolean
    },
    components: {
        Button
    },
    computed: {
        homePage() {
            const flag = (this.$route.path === '/') ? true : false
            return flag
        }
    }

}
</script>


<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>