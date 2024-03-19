<template>
  <div style="width: 100%">
    <div style="position: relative;">
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
        <div v-for="(item, index) in images" class="carousel-image-wrapper">
          <img
            :src="'images/' + item.name"
            :alt="item.alt"
            class="carousel-image"
          />
        </div>
      </div>
      <button @click="scrollNext()" id="button-next">Weiter</button>
      <button @click="scrollPrevious()" id="button-prev">Zurück</button>
    </div>
    <p>
      {{ text }}
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      images: [
        {
          name: "beispiel.jpg",
          alt: "beispiel",
        },
        {
          name: "modell.jpg",
          alt: "modell",
        },
        {
          name: "postcardTest.jpg",
          alt: "postcard Test",
        },
      ],
      text: "Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi. Lorem ipsum dolor sit amet,",
    };
  },
  methods: {
    scrollNext() {
      const width = document.querySelector('.carousel-image-wrapper').offsetWidth
      document.getElementById('carousel').scrollBy({
        left: width
      })
    },
    scrollPrevious() {
      const width = document.querySelector('.carousel-image-wrapper').offsetWidth
      document.getElementById('carousel').scrollBy({
        left: width * -1
      })
    }
  }
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
