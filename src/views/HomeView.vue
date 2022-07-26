<template>
  <div class="container">
    <Header title="Task tracker"/>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Header from '../components/Header.vue'
import Tasks from '../components/Tasks.vue'

export default defineComponent({
  name: 'HomeView',
  components: { Header, Tasks },
  data() {
    return {
      tasks: [] as any[],
    }
  },
  methods: {
    async deleteTask(id: Number) {
      if (confirm('Are you sure?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        })

        res.status === 200
          ? (this.tasks = this.tasks.filter((task: any) => task.id !== id))
          : alert('Error deleting task')
      }
    },
    async fetchTask(id: Number) {
      const res = await fetch(`api/tasks/${id}`)

      const data = await res.json()

      return data
    },
    async fetchTasks() {
        const res = await fetch('api/tasks')

        const data = await res.json()

        return data
    },
    async toggleReminder(id: Number) {
      const taskToToggle = await this.fetchTask(id)
      const updTask = { ...taskToToggle, reminder: !taskToToggle.reminder }

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updTask),
      })

      const data = await res.json()

      this.tasks = this.tasks.map((task: any) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      )
    },
  },
  async created() {
    this.tasks = await this.fetchTasks()
  },
})
</script>