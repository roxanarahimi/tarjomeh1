<template>
  <div id="services ">
    <div class="row justify-content-center text-center mb-5">
      <div class="col-12 col-lg-12 row justify-content-center">
        <div class="col-md-4 col-lg-3 px-lg-0 py-0 mb-3 py-lg-4">
          <div id="economic" class="card h-100 border border-primary ">
            <div class="card-body">
              <div class="card-small">
                <h3 class="text-primary">
                  Economic
                </h3>
                <small class="p">machine translation</small>
                <small class="p">Light review</small>
              </div>
              <h3 class="order-price">20 $</h3>
              <div class="text-center order-btn">
                <button class=" btn btn-primary text-light mx-auto">order</button>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-4 col-lg-4 p-lg-0 mb-3">
          <div id="professional" class="card h-100 border  border-primary   ">
            <div class="card-body">
              <div class="card-small">
                <h3 class="text-primary">Professional</h3>
                <small class="p">Translator</small>
                <small class="p">Quality Control</small>
              </div>
              <h3 class="order-price">30 $</h3>

              <div class="text-center order-btn">
                <button class=" btn btn-primary text-light mx-auto">order</button>
              </div>

            </div>
          </div>
        </div>
        <div class="col-md-4 col-lg-3 px-lg-0 py-0 mb-3 py-lg-4">
          <div id="premium" class="card h-100 border  border-primary">
            <div class="card-body">
              <h3 class="text-primary">Premium</h3>
              <div class="card-small">
                <small class="p">Translator</small>
                <small class="p">Specialist Editor</small>
                <small class="p">Quality Control</small>
              </div>
              <h3 class="order-price">50 $</h3>
              <div class="text-center order-btn">
                <button class=" btn btn-primary text-light mx-auto">order</button>
              </div>


            </div>
          </div>
        </div>

      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: "Services"
}
</script>

<style>
@media (min-width: 992px) {
  #economic {
    border-inline-end: 0 !important;
  }
  #premium {
    border-inline-start: 0 !important;
  }
}
</style>