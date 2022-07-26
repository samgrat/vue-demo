<template>
  <div class="container">
    <Header title="Task tracker"/>
    <Tasks :tasks="tasks" />
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