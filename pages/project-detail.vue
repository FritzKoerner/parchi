<template>
  <div style="width: 100%">
    <div
      style="
        height: 80vh;
        width: 100%;
        position: relative;
        overflow-y: hidden;
        overflow-x: scroll;
        display: flex;
      "
    >
      <img
        v-for="(item, index) in images"
        :src="'images/' + item.name"
        :alt="item.alt"
        class="carousel-image"
      />
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
};
</script>

<style>
.carousel-image {
  max-width: 100%;
  height: 100%;
  display: inline-block;
  width: auto;
}
</style>
