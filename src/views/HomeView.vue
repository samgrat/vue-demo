<template>
  <div class="container">
    <Header title="Task tracker"/>
    <Tasks @delete-task="deleteTask" :tasks="tasks" />
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
      tasks: [],
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
    async fetchTasks() {
        const res = await fetch('api/tasks')

        const data = await res.json()

        return data
    },
  },
  async created() {
    this.tasks = await this.fetchTasks()
  },
})
</script>