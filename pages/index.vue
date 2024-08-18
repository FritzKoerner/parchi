<template>
  <div class="wrapper-page">
    <h5 class="header-projects">Projekte...</h5>
    <div class="overview-grid">
      <ProjectCard v-for="proj in projects" :project="proj"></ProjectCard>
    </div>
  </div>
</template>

<script setup>
const { data: projects } = await useFetch("http://localhost:3030/projects");
</script>

<style>
.wrapper-page {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.overview-grid {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 8%;
}
.header-projects {
  display: none;
  font-size: 2rem;
  font-weight: 300;
  margin-top: 0;
  align-self: start;
}

@media (max-width: 768px) {
  .header-projects {
    display: block;
  }
}

@media (max-width: 1200px) {
  .overview-grid {
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr 1fr 1fr;
    gap: 4%;
  }
}
</style>
