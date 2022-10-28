<template>
  <div class="text-center bg-secondary pb-5 mb-5 mb-lg-0 ">
    <!--      <img style="width: 150px; opacity: 0.7" src="img/tarjomeh1white.png" alt="">-->
    <!--      <h2 class="text-center text-light" style="margin-top: 0px"> Professional translations made easy </h2>-->
    <!--      slide carousel-fade-->
    <div id="carouselExampleCaptions" class="carousel  carousel-dark  " data-bs-ride="carousel">
      <!--        <div class="carousel-indicators">-->
      <!--          <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>-->
      <!--          <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="1" aria-label="Slide 2"></button>-->
      <!--          <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="2" aria-label="Slide 3"></button>-->
      <!--        </div>-->
      <div class="carousel-inner" style="height: 200px">
        <div class="carousel-item active">
          <!--            <img src="..." class="d-block w-100" alt="...">-->
          <h3 class="px-5" style="padding-top: 100px;padding-bottom: 50px; text-align: center !important; width: 100%">Some representative placeholder</h3>
          <!--            <div class="carousel-caption d-none d-md-block">-->
          <!--              <h5>First slide label</h5>-->
          <!--              <p>Some representative placeholder content for the first slide.</p>-->
          <!--            </div>-->
        </div>
        <div class="carousel-item">
          <h3 class="px-5" style="padding-top: 100px;padding-bottom: 50px; text-align: center !important; width: 100%"> second slide.</h3>
          <!--            <div class="carousel-caption d-none d-md-block">-->
          <!--              <h5>Second slide label</h5>-->
          <!--              <p>Some representative placeholder content for the second slide.</p>-->
          <!--            </div>-->
        </div>
        <div class="carousel-item">
          <h3 class="px-5" style="padding-top: 100px;padding-bottom: 50px; text-align: center !important; width: 100%">representative placeholder content slide.</h3>
          <!--            <div class="carousel-caption d-none d-md-block">-->
          <!--              <h5>Third slide label</h5>-->
          <!--              <p>Some representative placeholder content for the third slide.</p>-->
          <!--            </div>-->
        </div>
      </div>
      <button class="carousel-control-prev mt-5" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide="prev">
        <span class="carousel-control-prev-icon text-dark" aria-hidden="true"></span>
        <span class="visually-hidden">Previous</span>
      </button>
      <button class="carousel-control-next mt-5" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide="next">
        <span class="carousel-control-next-icon text-dark" aria-hidden="true"></span>
        <span class="visually-hidden">Next</span>
      </button>
    </div>
  </div>

</template>

<script>
export default {
  name: "Slider"
}
</script>

<style scoped>

</style>