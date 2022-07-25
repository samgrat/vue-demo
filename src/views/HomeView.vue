<template>
  <div class="container">
    <Header title="Task tracker"/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Header from '../components/Header.vue'

export default defineComponent({
  name: 'HomeView',
  components: { Header }
})
</script>