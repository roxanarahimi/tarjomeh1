<template>
  <div  id="select"  class="rounded w-100 border-light bg-white py-1 px-3" style="height: 38px; cursor: pointer" @click="optionsToggle">
  <p v-show="selected" class="text-dark  d-inline-block">{{ selected.translate }}</p> <span class="text-primary float-end mt-1" style="font-size: 13px"><i class="bi bi-chevron-down"></i></span>



  <div v-show="showOptions"  @click="optionsTogglexx" class="rounded  border-light bg-white p-3 mt-3" id="options"  style="width:95%; min-height: 100px ; position: absolute; top: 110px;left:25px;box-shadow: 3px 3px 8px #888888;z-index: 2000">
    <div style="background-color: white; transform: rotate(45deg); position: relative;top:-20px; width: 10px;height: 10px"></div>
  <div class="d-flex flex-wrap justify-content-between text-dark ">
    <span v-for="item in data" class=" m-1 col-2 option1 text-start" @click="selectOption(item)" :class="{'btn btn-warning btn-sm text-light': item.language_id==selected.language_id}">{{ item.translate}}</span>
  </div>
</div>
</div>
</template>

<script>

import {onMounted, ref} from "vue";
export default {
  props:['data'],
  name: "VueSelect",
  setup(){
    const selected = ref({})
    const showOptions = ref(false)
    const optionsToggle = ()=>{
      showOptions.value = !showOptions.value;
    }
    const optionsTogglexx = () => { optionsToggle() }

    const selectOption = (item)=>{
      selected.value = item;
      console.log(selected.value)
    };
    onMounted(() => {
      // document.querySelector('#select:not(.selectedItems) ').addEventListener('click', optionsToggle);

      document.addEventListener('click',(event)=>{
        if(event.target.getAttribute('id') !== 'select'&& !event.target.classList.contains('option1')){
          showOptions.value = false;
        }else if(event.target.getAttribute('id') === 'select' || event.target.classList.contains('option1')){
          showOptions.value = true;

        }
      })
      });
    return{
      showOptions, optionsToggle, selected, selectOption, optionsTogglexx
    }
  }

}
</script>

<style scoped>

</style>