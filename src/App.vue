<template>
    <div id="app">
        <h1 class="text-center mb-2">Buscar usuario de GitHub</h1>
        <!-- TODO: Añadir componente GitHub -->
        <GitHub></GitHub>
    </div>
</template>

<script>
import GitHub from './components/GitHub.vue';
// TODO: Importar componente GitHub

export default {
    name: 'App',
    components: {
        // TODO: Añadir componente GitHub
        GitHub
    }
}
</script>

<style>
</style>
