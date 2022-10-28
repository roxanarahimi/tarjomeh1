<template>
  <div class="container-fluid" style="max-width:1200px; ">
    <top-menu/>
    <slider class="animate__animated animate__zoomIn"/>
    <main class="main mx-auto px-3 px-lg-0 " style="">
      <!--        <transitionGroup name = "switch" tag="div" mode = "out-in" appear>-->
<!--      <transition class="" name="fade" appear>-->
        <div>

          <router-view class="animate__animated animate__fadeInUp"  style="min-height: 428px !important" v-slot="{ Component }">
            <component :is="Component"></component>
          </router-view>


        </div>
<!--      </transition>-->
    </main>
  </div>
</template>
<script>
import TopMenu from "@/components/Menu";
import Slider from "@/components/Slider";
import {onMounted} from "vue";

export default {
  components: {Slider, TopMenu,},
    setup(){


    }
}
</script>
<style>


.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(20px);
}

.fade-enter-to,
.fade-leave-from {
  opacity: 1;
  transform: translateY(0px);
}

.fade-enter-active,
.fade-leave-active {
  transition: all 1s ease;
}

.switch-enter-from {
  opacity: 0;
  /* transform: scale(0, 1); */
  transform: translateY(50px);
}

.switch-leave-to {
  opacity: 0;
  transform: translateY(-50px);
}

.switch-enter-to,
.switch-leave-from {
  opacity: 1;
  transform: translateY(0px);
}

.switch-enter-active {
  transition: all 1s ease;
}

.switch-leave-active {
  transform: translateY(50px) !important;
  transition: all 1s ease;
  position: absolute !important;
}

.switch-move {
  transition: all 1s ease;
}

.fadeItems-enter-from,
.fadeItems-leave-to {
  opacity: 0;
  transform: scale(0, 0);
  transform: rotate(-20deg);
}

.fadeItems-enter-to,
.fadeItems-leave-from {
  opacity: 1;
  transform: scale(1, 1);
  transform: rotate(0deg);
}

.fadeItems-enter-active,
.fadeItems-leave-active {
  transition: all 1s ease;
}

.zoom-enter-from,
.zoom-leave-to {
  opacity: 0;
  transform: scale(0, 0);
}

.zoom-enter-to,
.zoom-leave-from {
  opacity: 1;
  transform: scale(1, 1);
}

.zoom-enter-active {
  transition: all 1s ease;
  animation-delay: 0.2;
}

.zoom-leave-active {
  transition: all 0.5s ease;
  transform: scale(0, 0) !important;
  position: absolute;
  right: calc(50% - 155px);
}

.zoom-move {
  transition: all 1s ease;
}

.route-enter-active,
.route-leave-active {
  transition: all 0.5s ease;
}

.route-enter-from,
.route-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

#outerr {
  overflow-x: hidden;
}


</style>
