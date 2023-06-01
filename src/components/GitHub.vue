<template>
    <div class="row container mx-auto">
        <input type="text" id="buscador" class="form-control">

        <div class="alert alert-danger mt-5" v-if="alerta" role="alert">
            El usuario no existe
        </div>

        <div v-else class="row mt-5">
            <div class="card col-xl-3 col-lg-5 col-md-7 col-sm-9 col-10 mx-auto" v-if="mostrarCard">
                <img :src="usuario.avatar_url" class="card-img-top" alt="...">
                <div class="card-body row">
                    <h5 class="card-title text-center">{{usuario.login}}</h5>
                    <button @click="obtenerRepositorios()" class="btn btn-primary mx-auto">Repositorios</button>
                    <a :href="'https://github.com/' + usuario.login" target="_blank" class="btn btn-light mx-auto mt-2">Url GitHub</a>

                </div>
            </div>
            <div v-if="mostrarLista" class="row">
                <div class="card col-4" >
                    <img :src="usuario.avatar_url" class="card-img-top" alt="...">
                    <div class="card-body">
                        <h5 class="card-title text-center">{{usuario.login}}</h5>
                        <button @click="obtenerRepositorios()" class="btn btn-primary col-6 mt-2">Repositorios</button>
                        <a :href="'https://github.com/' + usuario.login" target="_blank" class="btn btn-light col-6 mt-2">Url GitHub</a>

                    </div>
                </div>

                <GitHubRepos  :repolist="repolist" class="col-8"></GitHubRepos>
            </div>
            
        </div>
    </div>
</template>

<script>
import GitHubRepos from '/src/components/GitHubRepos.vue';
// TODO: Importar componente GitHubRepos

export default {
    name: 'GitHub',
    components: {
        // TODO: Importar componente GitHubRepos
        GitHubRepos
    },
    data: function() {
        return {
            // TODO: crear variables de datos para el funcionamiento del componente
            alerta: false,
            usuario: null,
            mostrarCard:false,
            mostrarLista : false,
            repos_url : "",
            repolist: []
        }
    },
    methods: {
        obtenerUsuario: function() {
        var url = 'https://api.github.com/users/';

        // Datos de autenticación
        /*var userAuth = process.env.VUE_APP_USERNAME || "JaviGva";
        var passAuth = process.env.VUE_APP_USERTOKEN || "Javi27520";

        var authString = userAuth + ':' + passAuth;
        var headers = new Headers();
        headers.append('Authorization', 'Basic ' + btoa(authString));
        headers.append('Content-Type', 'application/json');

        // Opciones de Fetch
        var fetchOptions = {
            method: 'GET',
            headers: headers,
            mode: 'cors',
            credentials: 'include'
        };*/


        fetch(url+document.getElementById("buscador").value)
            .then(response => {
                if (!response.ok) {
                    throw new Error('Network response was not ok');
                }
                return response.json();
            })
            .then(data => {
                this.usuario= data
                this.alerta = false
                this.mostrarCard = true
                this.mostrarLista = false
                this.repos_url = 'https://api.github.com/users/'+data.login+'/repos'
            })
            .catch(
                this.alerta=true,
                this.mostrarLista = false,
                this.mostrarCard = false
            );
        },
        obtenerRepositorios: function() {
            // TODO: Función para obtener los repositorios del usuario desde la API de GítHub
            
            this.mostrarCard=false
            this.mostrarLista = true

            fetch(this.repos_url)
                .then(response => {
                    if (!response.ok) {
                        throw new Error('Network response was not ok');
                    }
                    return response.json();
                })
                .then(data => {
                    this.repolist=data
                })
        }
    },
    mounted() {
        const vm = this;
        document.querySelector('#buscador').addEventListener('keypress', function (e) {
            if (e.key === 'Enter') {
                vm.obtenerUsuario();
            }
        });
    }

}




</script>

<style scoped>
</style>
