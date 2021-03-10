<template>
  <header>
      <h1>{{ title }}</h1>
      <p class="dark-mode-text">with Dark Mode</p>
      <Button 
        v-show="homePage"
        :text="showAddTask ? 'Close' : 'Add Task'"
        :color="showAddTask ? 'red' : 'green'"
        @btn-click="$emit('toggle-add-task')"
    />
  </header>
</template>

<script>
import Button from './Button'

export default {
    name: 'Header',
    props: {
        title: {
            type: String,
            default: 'Hello World'
        },
        showAddTask: Boolean
    },
    components: {
        Button
    },
    computed: {
        homePage() {
            if (this.$route.path === '/') {
                return true
            } else {
                return false
            }
        },
    },
}
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }

    .dark-mode-text {
        font-size: 0.7rem;
    }
</style>