<template>
    <div class="project-card">
        <h2 class="project-title">Projekttitel</h2>
        <!-- <div class="wrapper-image-card-project"> -->
            <img src="/images/beispiel.jpg" alt="oscar niemeyer paris" class="image-card-project">
        <!-- </div> -->
    </div>
</template>

<script>

</script>
<style>
.project-card:hover .project-title {
    transition: opacity 0.8s, top 0.5s;
    top: 0;
    opacity: 1;
}

.image-card-project {
    position: relative;
    z-index: 2;
    object-fit: cover;
    aspect-ratio: 13/8;
    height: 300px;
}

.project-title {
    z-index: 1;
    position: relative;
    top: 2rem;
    margin: 0;
    text-align: start;
    margin-bottom: 0.25rem;
    opacity: 0;
}
.project-subtitle {
    margin-bottom: 0.25rem;
}
</style>