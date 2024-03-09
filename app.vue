<template>
  <div id="layout-wrapper">
    <div id="contact-data">
      <div class="circle-blue"></div>
      <br />
      <p>
        <h4 style="text-align-last: center;">Paula Eden</h4> <br />
        Master Architektur <br />
        eden@gmx.de <br />
      </p>
    </div>
    <NuxtPage id="page-view"></NuxtPage>
  </div>
</template>

<script>
import "~/assets/css/main.css";
</script>
<style>
#contact-data {
  position: sticky;
  top: 30px;
  /* height: min-content; */
  text-align-last: justify;
  width: fit-content;
  white-space: nowrap;
}

.circle-blue {
  border-radius: 100%;
  background-color: #0000ff;
  width: 100%;
  aspect-ratio: 1/1;
}

#layout-wrapper {
  padding: 2rem;
  display: flex;
  height: 100vh;
  justify-content: space-evenly;
}
#page-view {
  padding-inline: 2rem;
}
</style>
