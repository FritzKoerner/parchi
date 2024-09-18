<template>
  <div>
    <div class="wrapper-flex-center">
      <div id="carousel">
        <div id="track">
          <img
            v-for="image in images"
            :src="`http://localhost:3030/projectFiles/${$route.params.id}/${image}`"
            :alt="image"
            class="carousel-image"
            draggable="false"
          />
        </div>
      </div>
    </div>
    <client-only>
      <div class="description-text">{{ text }}</div>
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
  data() {
    return {
      mouseDownAt: "0",
      prevPercentage: "0",
      precentage: "",
    };
  },
  mounted() {
    const track = document.getElementById("track");
    const handleOnDown = (e) => {
      this.mouseDownAt = e.clientX;
    };

    const handleOnUp = () => {
      this.mouseDownAt = "0";
      this.prevPercentage = this.percentage;
    };

    const handleOnMove = (e) => {
      if (this.mouseDownAt === "0") return;
      const mouseDelta = parseFloat(this.mouseDownAt) - e.clientX;
      const maxDelta = track.clientWidth * 1.1;
      const prevTemp = this.prevPercentage || "0"


      const percentage = (mouseDelta / maxDelta) * -100;
      const nextPercentageUnconstrained =
        parseFloat(prevTemp) + percentage;
      const nextPercentage = Math.max(
        Math.min(nextPercentageUnconstrained, 33),
        -33
      );

      this.percentage = nextPercentage;
      console.log(nextPercentage);
      track.animate(
        {
          transform: `translate(${nextPercentage}%, 0)`,
        },
        { duration: 1200, fill: "forwards" }
      );

      for (const image of track.getElementsByClassName("carousel-image")) {
        image.animate(
          {
            objectPosition: `${50 + nextPercentage}% center`,
          },
          { duration: 1200, fill: "forwards" }
        );
      }
    };

    /* -- Had to add extra lines for touch events -- */
    // window.addEventListener("mousedown", (e) => handleOnDown(e));
    window.onmousedown = (e) => handleOnDown(e);

    window.ontouchstart = (e) => handleOnDown(e.touches[0]);

    window.onmouseup = (e) => handleOnUp(e);

    window.ontouchend = (e) => handleOnUp(e.touches[0]);

    window.onmousemove = (e) => handleOnMove(e);

    window.ontouchmove = (e) => handleOnMove(e.touches[0]);
  },
};
</script>

<style>
#carousel {
  overflow: hidden;
}

#track {
  overflow: hidden;
  display: flex;
  gap: 8vmin;
}
.wrapper-flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.carousel-image {
  /* transform: translate(-50%, 0); */
  width: 33%;
  height: 70vh;
  object-fit: cover;
  object-position: center center;
}
.description-text {
  font-size: 1.2rem;
  padding: 1.8rem;
  white-space: pre;
}

</style>
