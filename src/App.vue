<script>
import ProjectCard from './components/ProjectCard.vue';
import Navbar from './components/Navbar.vue';

export default {
  name: "AppVue",
  data() {
    return {

    }
  },
  components: {
    ProjectCard,
    Navbar
}
}
</script>

<template>

  <header>
    <Navbar />
  </header>

  <router-view></router-view>

</template>

<style scoped>

</style>
