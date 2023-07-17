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
                projectPage: 0,
                projectTotalPages: 0,
            }
        },
        methods: {
            getProjectsData(){

            },
            
            getProjects(){
                this.loading = true;

                axios.get(this.apiUrl + "projects").then((response)=> {
                    this.projects = response.data.results.data;
                    this.projectPage = response.data.results.current_page;
                    this.projectTotalPages= response.data.results.last_page;
                    this.loading = false;
                }).catch(err=> {
                    this.loading = false;
                    this.loadingError = "Errore caricamento dati";
                })
            },

            nextPage(){

                if(this.projectPage < this.projectTotalPages){

                    let config = {
                        params: {
                            page: (this.projectPage + 1)
                        }
                    };

                    this.loading = true;

                    axios.get(this.apiUrl + "projects", config).then((response)=> {
                        this.projects = response.data.results.data;
                        this.projectPage = response.data.results.current_page;
                        this.projectTotalPages= response.data.results.last_page;
                        this.loading = false;
                    }).catch(err=> {
                        this.loading = false;
                        this.loadingError = "Errore caricamento dati";
                    })
                } else{
                    console.error("Non ci sono più pagine")
                }
            },

            previusPage(){

                if(this.projectPage > 0){

                    let config = {
                        params: {
                            page: (this.projectPage - 1)
                        }
                    };

                    this.loading = true;

                    axios.get(this.apiUrl + "projects", config).then((response)=> {
                        this.projects = response.data.results.data;
                        this.projectPage = response.data.results.current_page;
                        this.projectTotalPages= response.data.results.last_page;
                        this.loading = false;
                    }).catch(err=> {
                        this.loading = false;
                        this.loadingError = "Errore caricamento dati";
                    })
                } else{
                    console.error("Non ci sono più pagine")
                }
            },

            page(pageNumber){

                if(pageNumber <= this.projectTotalPages){

                    let config = {
                        params: {
                            page: pageNumber
                        }
                    };

                    this.loading = true;

                    axios.get(this.apiUrl + "projects", config).then((response)=> {
                        this.projects = response.data.results.data;
                        this.projectPage = response.data.results.current_page;
                        this.projectTotalPages= response.data.results.last_page;
                        this.loading = false;
                    }).catch(err=> {
                        this.loading = false;
                        this.loadingError = "Errore caricamento dati";
                    })
                } else{
                    console.error("Non ci sono più pagine")
                }
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
        <h4>Page:{{ projectPage }} di {{ projectTotalPages }}</h4>

        <div v-for="project in projects">
            <h2>{{ project.title }}</h2>
            <p>CATEGORIA: {{ project.category ? project.category.name : "Nessuna categoria" }}</p>
            <p>TECNOLOGIE:
                <span v-if="project.technologys.length" v-for="tech in project.technologys" > {{ tech }} </span>
                <span v-else>Nessuna</span>
            </p>
            <p>DESCRIZIONE:{{ project.content }}</p>

        </div>

        <a @click="previusPage()">Prev</a>

        <a @click="page(pageNumber)" v-for="pageNumber in projectTotalPages">bottone{{ pageNumber }} </a>

        <a @click=" nextPage()">Next</a>

    </main>

</template>

<style scoped>

</style>