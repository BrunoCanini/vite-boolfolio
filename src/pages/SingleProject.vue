<script>
import axios from 'axios';

    export default {
        name: "SingleProject",
        data(){
            return{
                loading: false,
                apiUrl: "http://127.0.0.1:8000/api/",
                imageUrl: "http://127.0.0.1:8000/storage/",
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
        },
        beforeRouteUpdate (to,from){
            if(from.name == to.name){
                let newProjectId = to.params.id;
                this.getProject(newProjectId)
            }
        }
    }

</script>

<template>

    <section v-if="project">

        <div class="card m-3" style="width: 18rem;">
            <img :src="imageUrl + project.image" class="card-img-top" alt="">
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

    </section>

</template>


<style scoped>

</style>