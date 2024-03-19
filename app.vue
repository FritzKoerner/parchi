<template>
  <div id="layout-wrapper">
    <div id="contact-data-wrapper">
      <div id="contact-data">
        <div class="circle-blue"></div>
        <br />
        <p>
          <h4 style="text-align-last: center;"><strong>Paula Eden</strong></h4> 
          <br />
          Master Architektur <br />
          eden@gmx.de <br />
          +491242133123 <br>
        </p>
        <a style="display: flex; align-items: center; justify-content: space-between;">
          <p style="text-transform: uppercase;"><strong>Portfolio</strong></p>  
          <img src="/png/download.png" alt="download button" style=" height: 1.25rem;">
        </a>
      </div>
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
  padding: 5rem;
  display: flex;
  justify-content: space-between;
}
#page-view {
  padding-left: 4rem;
}

@media (max-width: 768px) {
  #layout-wrapper {
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 2rem;
  }  
  #contact-data {
    margin-bottom: 4rem
  }
  #page-view {
    padding: 0;
  }  
  }
</style>
