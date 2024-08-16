<template>
  <div style="width: 100%">
    <div style="position: relative">
      <div
        style="
          height: 80vh;
          width: 100%;
          position: relative;
          overflow-y: hidden;
          overflow-x: scroll;
          display: flex;
          scroll-snap-type: x mandatory;
        "
        id="carousel"
      >
        <div v-for="image in images" class="carousel-image-wrapper">
          <img
            :src="`http://localhost:3030/projectFiles/${$route.params.id}/${image}`"
            :alt="image"
            class="carousel-image"
          />
        </div>
      </div>
      <svg
        width="80"
        height="80"
        xmlns="http://www.w3.org/2000/svg"
        @click="scrollNext()"
        id="button-next"
      >
        <defs>
          <filter id="f1">
            <feDropShadow dx="2" dy="5" stdDeviation="2" flood-opacity="0.3" />
          </filter>
        </defs>
        <polygon
          points="50,24 0,0 0,50"
          style="fill: #0000ff"
          filter="url(#f1)"
          transform="translate(15, 15)"
        />
      </svg>
      <svg
        width="80"
        height="80"
        xmlns="http://www.w3.org/2000/svg"
        @click="scrollPrevious()"
        id="button-prev"
      >
        <defs>
          <filter id="f2">
            <feDropShadow dx="3" dy="5" stdDeviation="2" flood-opacity="0.3" />
          </filter>
        </defs>
        <polygon
          points="0,24 50,0 50,50"
          style="fill: #0000ff"
          filter="url(#f2)"
          transform="translate(15, 15)"
        />
      </svg>
    </div>
    <client-only>
      <div style="white-space: pre">{{ text }}</div>
    </client-only>
  </div>
</template>

<script setup>
const route = useRoute();
const { data: images } = await useLazyFetch(
  `http://localhost:3030/projects/${route.params.id}`
);
const { data: text } = await useLazyFetch(
  `http://localhost:3030/projectFiles/${route.params.id}/desc.txt`
);
</script>

<script>
export default {
  methods: {
    scrollNext() {
      let width = document.querySelector(".carousel-image-wrapper").offsetWidth;

      const carouselElement = document.getElementById("carousel");
      console.log(carouselElement.scrollLeft);
      console.log(width);
      console.log(carouselElement.scrollLeft < width);
      if (carouselElement.scrollLeft < width) {
        width = width * 2;
      }
      console.log(carouselElement.scrollLeft);
      console.log(width);
      console.log(carouselElement.scrollLeft < width);
      carouselElement.scrollBy({
        left: width,
      });
    },
    scrollPrevious() {
      const width = document.querySelector(
        ".carousel-image-wrapper"
      ).offsetWidth;
      document.getElementById("carousel").scrollBy({
        left: width * -1,
      });
    },
  },
};
</script>

<style>
#button-prev {
  position: absolute;
  top: 50%;
  left: 10px;
  transform: translateY(-50%);
}

#button-next {
  position: absolute;
  top: 50%;
  right: 10px;
  transform: translateY(-50%);
}
.carousel-image-wrapper {
  padding: 0.5rem;
  width: 100%;
  flex-shrink: 0;
  scroll-snap-align: center;
  display: flex;
  justify-content: center;
  scroll-snap-stop: always;
}

@media (max-width: 768px) {
  .carousel-image-wrapper {
    padding: 0;
  }
}
.carousel-image {
  max-width: 100%;
  object-fit: contain;
  height: 100%;
}
</style>
