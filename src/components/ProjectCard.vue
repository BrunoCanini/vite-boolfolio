<script>
import axios from 'axios';


    export default {
        name: "ProjectCard",
        data() {
            return{
                apiUrl: "http://127.0.0.1:8000/api/",
                loading: false,
                loadingError: false,
                projects: [],
            }
        },
        methods: {
            getProjects(){
                this.loading = true;
                axios.get(this.apiUrl + "projects").then((response)=> {
                    // console.log(response.data);
                    this.projects = response.data.results.data;
                    this.loading = false;
                }).catch(err=> {
                    this.loading = false;
                    this.loadingError = "Errore caricamento dati";
                })
            }

        },
        mounted() {
            this.getProjects();
        }
    }

</script>

<template>

    <main>
        <h3 v-if="loading" >Caricamento in corso</h3>
        <h3 v-if="loadingError" >{{loadingError}}</h3>

        <div v-for="project in projects">
            <h2>{{ project.title }}</h2>
            <p>CATEGORIA: {{ project.category ? project.category.name : "Nessuna categoria" }}</p>
            <p>TECNOLOGIE:
                <span v-if="project.technologys.length" v-for="tech in project.technologys" > {{ tech }} </span>
                <span v-else>Nessuna</span>
            </p>
            <p>DESCRIZIONE:{{ project.content }}</p>

        </div>

    </main>

</template>

<style scoped>

</style>