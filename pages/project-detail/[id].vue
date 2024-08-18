<template>
  <div>
    <div class="wrapper-flex-center">
      <div id="carousel" data-mouse-down-at="0" data-prev-percentage="0">
        <!-- <div v-for="image in images" class="carousel-image-wrapper">
          <img
            :src="`http://localhost:3030/projectFiles/${$route.params.id}/${image}`"
            :alt="image"
            class="carousel-image"
          />
        </div> -->
        <img
          v-for="image in images"
          :src="`http://localhost:3030/projectFiles/${$route.params.id}/${image}`"
          :alt="image"
          class="carousel-image"
          draggable="false"
        />
      </div>
      <!-- <svg
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
      </svg> -->
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
  mounted() {
    const track = document.getElementById("carousel");
    const handleOnDown = (e) => {
      track.dataset.mouseDownAt = e.clientX;
      console.log(track);
    };

    const handleOnUp = () => {
      track.dataset.mouseDownAt = "0";
      track.dataset.prevPercentage = track.dataset.percentage;
    };

    const handleOnMove = (e) => {
      if (track.dataset.mouseDownAt === "0") return;

      const mouseDelta = parseFloat(track.dataset.mouseDownAt) - e.clientX,
        maxDelta = track.innerWidth / 2;

      const percentage = (mouseDelta / maxDelta) * -100,
        nextPercentageUnconstrained =
          parseFloat(track.dataset.prevPercentage) + percentage,
        nextPercentage = Math.max(
          Math.min(nextPercentageUnconstrained, 0),
          -100
        );

      track.dataset.percentage = nextPercentage;

      // track.animate(
      //   {
      //     transform: `translate(${nextPercentage}%, -50%)`,
      //   },
      //   { duration: 1200, fill: "forwards" }
      // );

      // for (const image of track.getElementsByClassName("carousel-image")) {
      //   image.animate(
      //     {
      //       objectPosition: `${100 + nextPercentage}% center`,
      //     },
      //     { duration: 1200, fill: "forwards" }
      //   );
      // }
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
  methods: {
    scrollNext() {
      const width = document.querySelector(
        ".carousel-image-wrapper"
      ).offsetWidth;
      document.getElementById("carousel").scrollBy({
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

#carousel {
  overflow: hidden;
  display: flex;
  gap: 4vmin;
}
.wrapper-flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.carousel-image-wrapper {
  width: 100%;
  flex-shrink: 0;
  display: flex;
  justify-content: center;
}

@media (max-width: 768px) {
  .carousel-image-wrapper {
    padding: 0;
  }
}
.carousel-image {
  width: 40vmin;
  height: 70vh;
  object-fit: cover;
  object-position: 100% center;
}
</style>
