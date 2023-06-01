<template>
    <div>
    <ul class="list-group">
      <li class="list-group-item d-flex justify-content-between align-items-start" v-for="repo in repolist" :key="repo.id" :title="repo.description">
        <a class="ms-2 me-auto text-decoration-none text-black" :href="repo.html_url" target="_blanck">
            {{ repo.full_name }}
        </a>
        <span class="badge bg-primary rounded-pill">{{repo.forks}}</span>
      </li>
            
            
    </ul>
  </div>
</template>

<script>
export default {
    name: 'GitHubRepos',
    props: ['repolist'],
    data: function() {
        return {
            // TODO: crear variables de datos para el funcionamiento del componente
            
        }
    }
}
</script>

<style scoped>
</style>
