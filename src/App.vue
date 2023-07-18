<script>
import ProjectCard from './components/ProjectCard.vue'

export default {
  name: "AppVue",
  data() {
    return {

    }
  },
  components: {
    ProjectCard
  }
}
</script>

<template>

  <header>
    <h1>menu</h1>
  </header>

  <router-view></router-view>

</template>

<style scoped>

</style>
