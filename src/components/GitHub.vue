<template>
    <div>
        <!-- TODO: Crear componente GitHub -->
        <input type="text" placeholder="Introduce tú nombre de usuario de GitHub"  v-model="user"  v-show="input" v-on:keydown="obtenerUsuario"/>
        <div class="alert alert-warning" role="alert" v-show="!input"> El usuario no existe </div>
        <div class="card" style="width: 18rem;" v-show="input">
            <img class="card-img-top" src="userData.avatar_url" alt="Card image cap"> //foto avatar
            <div class="card-body">
                <h5 href="userData.login" class="card-title"></h5> //login del usuario
                <button type="button" class="btn btn-primary" v-on:keydown="obtenerUsuario">Repositorios</button>// llamar al método obtenerRepositorios cuando se pulse.
                <a href="userData.html_url" class="card-link">URL de Github</a>
            </div>
        </div>
        
    </div>
</template>

<script>

// TODO: Importar componente GitHubRepos

import GitHubRepos from './GitHubRepos.vue'

export default {
    name: 'GitHub',
    components: {
        // TODO: Importar componente GitHubRepos
        GitHubRepos
    },
    data: function() {
        return {
            // TODO: crear variables de datos para el funcionamiento del componente
            user: 'vuejs',
            input: true,    
            card: false,
            userData: ""
            repolist: 
        }
    },
    methods: {
        obtenerUsuario: function() {
            // TODO: Función para obtener los datos de usuario de la API de GitHub

            // TODO: Añadir lógica para resetear los cambios en el interfaz: desactivar campo de envío,
            // resetear mensaje de error, mostrar lista de repositorios,...

            // Obtener datos de autenticación de usuario para hacer peticiones
            // autenticadas a la API de GitHub
            var userAuth = process.env.VUE_APP_USERNAME || "user";
            var passAuth = process.env.VUE_APP_USERTOKEN || "pass";

            // TODO: realizar petición fetch par obtener los datos y mostrar la información en la página
            // Ejemplo de paso de datos de autorización con fetch: https://stackoverflow.com/questions/43842793/basic-authentication-with-fetch
            let url="https://api.github.com/users/{{user}}";
            fetch(url, {method:'GET',})
            .then(response => response.json())
            .then(data => {
                const login = data.login;
                const avatar = data.avatar_url;
                const html_url = data.html_url;
                const repos_url = data.repos_url;
            });

        },
        obtenerRepositorios: function() {
            // TODO: Función para obtener los repositorios del usuario desde la API de GítHub
            // La URL de los repositorios de usuario se puede obtener a través del campo 'repos_url' de los datos del usuario

            // Obtener datos de autenticación de usuario para hacer peticiones
            // autenticadas a la API de GitHub
            var userAuth = process.env.VUE_APP_USERNAME || "user";
            var passAuth = process.env.VUE_APP_USERTOKEN || "pass";


            // TODO: realizar petición fetch par obtener los datos y mostrar la información en la página
            // Ejemplo de paso de datos de autorización con fetch: https://stackoverflow.com/questions/43842793/basic-authentication-with-fetch
            let url="https://api.github.com/users/{{user}}";
            let username = 'user';
            let password = 'pass';

            ////headers.append('Content-Type', 'text/json');
            let headers: {'Authorization': 'Basic ' + btoa('login:password')}});

            fetch(url, {method:'GET',
                       headers: headers})
            .then(response => response.json())
            .then(data => {
                const full_name = data.full_name;
                const html_url = data.html_url;
                const description = data.description;
                const forks_count = data.forks_count;
            });
        }
    }
}
</script>

<style scoped>
</style>
<! --
https://www.youtube.com/watch?v=2NZtT6EXRos
https://www.youtube.com/watch?v=n1k2wruzhW0

- v-model: directiva que crea una sincronia entre el campo y la propiedad que esta dentro de 
         data(){}
- v-show="" = if solo que este utiliza display:none cuando no existe
              se utiliza para ocultar o mostrar (para elementos que cambian)
- v-model="user" conexion directa entre input y el js
-->