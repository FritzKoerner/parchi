<template>
  <div class="wrapper-page">
    <div class="overview-grid">
      <ProjectCard></ProjectCard>
      <ProjectCard></ProjectCard>
      <ProjectCard></ProjectCard>
      <ProjectCard></ProjectCard>
    </div>
  </div>
</template>

<style>
.wrapper-page {
  display: flex;
  justify-content: center;
}
.overview-grid {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 8%;
}

@media (max-width: 1200px) {
  .overview-grid {
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr 1fr 1fr;
    gap: 4%;
  }
}
</style>
