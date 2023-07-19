<script>

    export default {
        name: "Navbar",
        data() {
            return {
                navLinks: [
                    {route: "home", label: "Home"},
                    {route: "about", label: "About"},
                    {route: "projects", label: "Projects", params: {code:"-my-projects"} },
                ]
            };
    },
}

</script>

<template>

    <nav class="navbar navbar-expand-lg bg-body-tertiary">
        <div class="container-fluid">
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav" v-for="link in navLinks">
                    <li class="nav-item">
                        <router-link :to="{name: link.route, params: link.params}" class="nav-link active" aria-current="page">{{link.label}}</router-link>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

</template>

<style scoped>

</style>