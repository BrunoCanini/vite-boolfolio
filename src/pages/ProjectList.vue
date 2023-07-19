<script>

import ProjectCard from '../components/ProjectCard.vue';

    export default {
    name: "ProjectList",
    data() {
        return {};
    },
    components: { ProjectCard }
}

</script>

<template>

    <section>
        <h1 class="mx-4">Projects:</h1>
        <ProjectCard />
    </section>

</template>

<style scoped>

</style>