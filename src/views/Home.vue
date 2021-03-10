<template>
    <AddTask v-if="showAddTask" @add-task="addTask" />
    <Tasks :tasks="tasks" @toggle-reminder="toggleReminder" @delete-task="deleteTask" />
</template>

<script>

import AddTask from '../components/AddTask'
import Tasks from '../components/Tasks'

export default {
    name: 'Home',
    components: {
        Tasks,
        AddTask
    },
    props: {
        showAddTask: Boolean,
    },
    data() {
        return {
            tasks: [],
        }
    },
    async created() {
        this.tasks = await this.fetchTasks()
    },
    methods: {
        addTask: async function(task) {
            const res = await fetch('api/tasks', {
                method: 'POST',
                headers: {
                'Content-type': 'application/json',
                },
                body: JSON.stringify(task)
            })
            const data = await res.json()

            this.tasks = [...this.tasks, data]
        },
        deleteTask: async function(id) {
            if(confirm("Are you sure want to delete this task?")){

                const res = await fetch(`api/tasks/${id}`, {
                method: 'DELETE'
                })

                res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert('Error deleting task')
            }
        },
        toggleReminder: async function(id) {
            const taskToToggle = await this.fetchTask(id)
            const updTask = {...taskToToggle, reminder: !taskToToggle.reminder}

            const res = await fetch(`api/tasks/${id}`, {
                method: 'PUT',
                headers: {
                'Content-type': 'application/json'
                },
                body: JSON.stringify(updTask)
            })

            const data = await res.json()

            this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder} : task)
        },
        fetchTasks: async function() {
            const res = await fetch('api/tasks')

            const data = await res.json()

            return data
        },
        fetchTask: async function(id) {
            const res = await fetch(`api/tasks/${id}`)
            const data = await res.json()
            return data
        },
    }
}
</script>

<style>

</style>