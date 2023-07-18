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
        <span>Page:{{ projectPage }} di {{ projectTotalPages }}</span>

        <div class="d-flex m-4">
            <div v-for="project in projects" class="card m-2" style="width: 18rem;">
                <div class="card-body">
                    <h5 class="card-title">{{ project.title }}</h5>
                    <p class="card-text">CATEGORIA: {{ project.category ? project.category.name : "Nessuna categoria" }}</p>
                    <p class="card-text">TECNOLOGIE:
                        <span v-if="project.technologys.length" v-for="tech in project.technologys" class="card-text" > {{ tech.name }} </span>
                        <span v-else class="card-text">Nessuna</span>
                    </p>
                    <p class="card-text">DESCRIZIONE:{{ project.content }}</p>
                </div>
            </div> 
        </div>

        <div class="text-center">
            <a @click="previusPage()" class="btn btn-primary m-2">Prev</a>
            <a @click="page(pageNumber)" v-for="pageNumber in projectTotalPages" class="btn btn-primary m-2">bottone{{ pageNumber }} </a>
            <a @click=" nextPage()" class="btn btn-primary m-2">Next</a> 
        </div>

    </main>

</template>

<style scoped>

</style>