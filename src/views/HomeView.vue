<template>

  <div class="home">

    <main-form/>

    <services class="d-none"/>
  </div>
</template>

<script>
// @ is an alias to /src


import {onMounted} from "vue";
import MainForm from "@/components/Form";
import Services from "@/components/Services";

export default {
  name: 'HomeView',
  components: {MainForm, Services},
  setup() {
    onMounted(() => {

    })


    return {

    }
  }
}
</script>

<style>
h3 {
  text-align: center;
}

.p {
  width: 100%;
  text-align: center !important;
  display: block;
  color: rgba(255, 255, 255, 0.5);
  /*color: rgba(0, 0, 0, 0.5);*/
}

.card-small {
  height: 100px;
  margin-bottom: 20px;

}

.card-body {
  display: grid !important;
}

.order-btn, .order-price {
  display: grid !important;
  align-self: end !important;

}

.order-btn button {

  height: 40px;
  align-self: end !important;

}

body {
  background-color: whitesmoke;

}

select {
  padding-right: 30px !important;
}

.card, .navbar {
  /*background-color: rgba(255, 255, 255, 0.44) !important;*/
  color: white !important;
  background-color: rgba(0, 0, 0, 0.4) !important;
}

.card {

}

input, select, textarea {
  /*background: rgba(255, 255, 255, 0.18) !important;*/
  /*color: white!important;*/
  /*height: 50px;*/
}

.card, label {
  color: rgba(255, 255, 255, 0.9) !important;
  text-align: left;
}

input, select, textarea {
  /*height: 100px;*/
  /*border-radius: 0px !important;*/
}

.navbar {
  background: #2c3034 !important;

}

.navbar ul li a:not(.text-primary) {
  color: rgba(255, 255, 255, 0.9) !important;
}
</style>