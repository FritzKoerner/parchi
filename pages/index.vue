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
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    column-gap: 5%;
}
</style>