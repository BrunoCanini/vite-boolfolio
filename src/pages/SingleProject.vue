<script>
import axios from 'axios';

    export default {
        name: "SingleProject",
        data(){
            return{
                loading: false,
                apiUrl: "http://127.0.0.1:8000/api/",
                loadingError: false,
                project: null
            }
        },
        methods: {
            getProject(id) {
                this.loading = true;

                axios.get(this.apiUrl + "projects/" + id).then((response)=> {
                    this.project = response.data.results;
                    this.loading = false;
                }).catch(err=> {
                    this.loading = false;
                    this.loadingError = "Errore caricamento dati";
                    this.$router.push({ name: "error"});
                })
            }
        },
        mounted() {
            this.getProject(this.$route.params.id);
        }
    }

</script>

<template>

    <section v-if="project">
        <div class="d-flex m-4">
            <div class="card m-2" style="width: 18rem;">
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
    </section>

</template>

<style scoped>

</style>