<template>
  <div id="multiSelect" class="rounded w-100 border-light bg-white pt-1  px-3" style="min-height: 38px; cursor: pointer">
    <span class="text-primary float-end mt-1" style="font-size: 13px"><i class="bi bi-chevron-down"></i></span>
    <span v-for="selected in selectedItems"  class="btn btn-sm btn-primary text-light px-3 me-2 mb-1 selectedItems">{{ selected.translate }}
    <i class="bi bi-x" @click="removeItem(selected.id)"></i>
  </span>

    <div v-show="showMultiOptions" @click="optionsTogglexx" class="rounded  border-light bg-white p-3 mt-3"
         id="optionsz"  style="width:95%; min-height: 100px ; position: absolute; top: 110px;left:25px;box-shadow: 3px 3px 8px #888888;z-index: 2000">
      <div style="background-color: white; transform: rotate(45deg); position: relative;top:-20px;left:50%;width: 10px;height: 10px"></div>

      <div class="d-flex flex-wrap justify-content-between text-dark ">
        <span v-for="item in data" class=" m-1 col-2 option text-start" :id="'option_' + item.id" @click="selectOption(item)">{{ item.translate }}</span>
      </div>
    </div>
  </div>
</template>

<script>

import {onMounted, ref} from "vue";

export default {
  props: ['data'],
  name: "VueMultiSelect",
  setup() {
    const selectedItems = ref([])
    const showMultiOptions = ref(false)
    const openOptions = () => {   showMultiOptions.value = true;    };
    const optionsToggle = () => {  showMultiOptions.value = !showMultiOptions.value; }
    const selectOption = (item) => {
      selectedItems.value.push(item);
      let opt = document.querySelector('#option_'+item.id);

      if(opt.classList.contains('btn-primary')){
        opt.classList.remove('btn')
        opt.classList.remove('btn-primary')
        opt.classList.remove('btn-sm')
        opt.classList.remove('text-light')
      }else {
        opt.classList.add('btn')
        opt.classList.add('btn-primary')
        opt.classList.add('btn-sm')
        opt.classList.add('text-light')
      }

    }
    const optionsTogglexx = () => { optionsToggle() }
    const removeItem = (id) => {
      let i = 0;
      selectedItems.value.forEach((element) => {
        if (element.id === id) {  selectedItems.value.splice(i, 1); }
        i++;
      })
      console.log(selectedItems.value);
      showMultiOptions.value=false;

    }

    onMounted(() => {
      // document.querySelector('#multiSelect:not(.selectedItems) ').addEventListener('click', optionsToggle);

      document.addEventListener('click',(event)=>{
        if(event.target.getAttribute('id') !== 'multiSelect'&& !event.target.classList.contains('option')){
          showMultiOptions.value = false;
        }else if(event.target.getAttribute('id') === 'multiSelect' || event.target.classList.contains('option')){
        showMultiOptions.value = true;

        }
      })
      // let x = document.querySelector('body:not(#multiSelect)');

      document.addEventListener('click', ()=>{});

    })
    return {
      showMultiOptions, optionsToggle, selectedItems, selectOption, openOptions, optionsTogglexx, removeItem
    }
  }

}
</script>

<style scoped>

</style>