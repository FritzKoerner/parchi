<template>
  <NuxtLink class="project-card" :to="`project-detail/${id}`">
    <h2 class="project-title">Projekttitel</h2>
    <!-- <div class="wrapper-image-card-project"> -->
    <img
      src="/images/beispiel.jpg"
      alt="oscar niemeyer paris"
      class="image-card image-card-front"
    />
    <img
      src="/images/postcardTest.jpg"
      alt="child on street"
      class="image-card image-card-back"
    />
    <!-- </div> -->
  </NuxtLink>
</template>

<script>
export default {
  props: {
    id: {
      type: String,
      required: true,
    },
  },
};
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
