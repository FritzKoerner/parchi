<template>
  <NuxtLink class="project-card" :to="`project-detail/${project}`">
    <h2 class="project-title">{{ project }}</h2>
    <div class="wrapper-image-card-project">
      <img
        :src="`http://localhost:3030/projectFiles/${project}/${imageFront}`"
        :alt="imageFront"
        class="image-card image-card-front"
      />
      <img
        :src="`http://localhost:3030/projectFiles/${project}/${imageBack}`"
        :alt="imageBack"
        class="image-card image-card-back"
      />
    </div>
  </NuxtLink>
</template>

<script setup>
const props = defineProps({
  project: {
    type: String,
    required: true,
  },
});
const { data: images } = await useFetch(
  `http://localhost:3030/projects/${props.project}`
);
const values = images.value;
const imageFront = values[0];
const imageBack = values[1] ?? images[0];
</script>

<style>
.project-card {
  margin: 0;
  padding: 0;
  position: relative;
  text-decoration: none;
  color: black;
}
.project-card:hover {
  cursor: url(SVG/cursor-pointer.svg), pointer;
}

.project-card:hover .project-title {
  transition: opacity 0.8s, top 0.5s;
  top: -2rem;
  opacity: 1;
}

.project-card:hover .image-card-front {
  transition: opacity 1s;
  opacity: 0;
}
.image-card {
  object-fit: cover;
  aspect-ratio: 13/8;
  max-width: 100%;
  max-height: 100%;
  width: 100%;
  margin: 0;
}
.image-card-front {
  position: relative;
  z-index: 2;
}

.image-card-back {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 0;
}

.project-title {
  z-index: 1;
  position: absolute;
  top: 0;
  margin: 0;
  text-align: start;
  opacity: 0;
}
.project-subtitle {
  margin-bottom: 0.25rem;
}
</style>
