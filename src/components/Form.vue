<template>
  <div class="row justify-content-center px-2">
    <div id="frame" class="card shadow-none border-0 mb-5 py-4 px-3 mt-5"
         style="background-color: rgba(0,0,0,0.4); transition: all 1s ease">
      <div id="main-card" class="card-body ">
        <form id="maniForm" class="" action="">
          <div class="row">
            <div class="col-md-6 col-lg-4">
              <label class="form-label mt-2">from </label>
              <vue-select :data="translates" />
            </div>
            <div class="col-md-6 col-lg-4">
              <label class="form-label mt-2">to </label>
              <vue-multi-select :data="translates" />
            </div>
            <div v-show="false" class="col-md-6 col-lg-4">
              <label for="from" class="form-label">from </label>
              <select @change="checkFromTo('from')" id="from" class="form-select">
<!--                <option value=""></option>-->
<!--                <option selected id="from_english" value="english">english</option>-->
                <option v-for="item in translates" :value="item.id">{{  item.translate }}</option>
              </select>
            </div>

            <div v-show="false" class="col-md-6 col-lg-4">
              <label for="to" class="form-label">to</label>
              <select @change="checkFromTo('to')" id="to" class="form-select">
                <option value=""></option>
                <option v-for="item in translates" :key="item.id" :value="item.id" class=" text-center">{{ item.translate }}</option>

              </select>
            </div>
            <div class="col-md-6 col-lg-4">
              <label for="subject" class="form-label">subject</label>
              <select @change="estimate" id="subject" class="form-select">
                <option data-price="1">general</option>
                <option data-price="2">medical</option>
                <option data-price="1">sci fi</option>
                <option data-price="1.5">computer</option>
                <option data-price="1">art</option>
              </select>
            </div>


            <div id="selectSection" v-show="!typeSelected" class="col-lg-12 animate__animated px-4"
                 style="transition: 1s ease all">
              <label class="form-label">&nbsp;</label>
              <div id="selectType" class="row bg-white rounded p-4 py-lg-0 animate__animated"
                   style="min-height: 200px;font-size: 50px !important;">
                <button @click.prevent="selectType('text')"
                        class="btn-select btn btn-primary btn col-md-5 text-black-50 ">Type Text
                </button>
                <span class="col-md-2 text-center or text-black-50 ">or</span>
                <button @click.prevent="selectType('file')"
                        class="btn-select btn btn-primary btn col-md-5 text-black-50">Upload File
                </button>
              </div>
            </div>
            <div id="textSection" v-show="typeIsText && typeSelected" class="col-lg-12 animate__animated"
                 style="transition: 1s ease all">
              <label for="text" class="form-label">text</label>
              <div class="text-end" style="margin-bottom: -32px; margin-right: 1px">
                <button @click.prevent="txtFileToggle" class="btn btn-primary btn-sm px-5 text-light" style=""><i
                    class="bi bi-arrow-left-right"></i> file mode
                </button>
              </div>
              <textarea @input="countText" rows="6" style="min-height: 200px" id="text"
                        class="pt-5 form-control"></textarea>
            </div>
            <div id="fileSection" v-show="!typeIsText && typeSelected" class="col-lg-12 animate__animated"
                 style="transition: 1s ease all">
              <label class="form-label">file</label>
              <div class="text-end" style="margin-bottom: -32px; margin-right: 1px">
                <button @click.prevent="txtFileToggle" id="changeToText" class="btn btn-primary btn-sm px-5 text-light" style=""><i
                    class="bi bi-arrow-left-right"></i> text mode
                </button>
              </div>
              <drop-zone/>
            </div>

            <div style="z-index: 1000" class="col-md-6 col-lg-6">
              <label for="count" class="form-label">word count</label>
              <input @change="estimate" disabled type=text id="count" class="form-control" value="0">
            </div>
            <div style="z-index: 1000" class="col-md-6 col-lg-6">
              <label for="service" class="form-label">service</label>
              <select @change="estimate" id="service" class="form-select">
                <option data-price="20">economic</option>
                <option data-price="30">professional</option>
                <option data-price="50">premium</option>
              </select>
            </div>
          </div>
          <div class="row d-none">
            <div class="col-md-5">
              <label for="date" class="form-label">delivery date</label>
              <input type=text id="date" class="form-control" value="">
            </div>
            <div class="col-md-5">
              <label for="cost" class="form-label">estimated cost</label>
              <input type=text id="cost" class="form-control" v-model="cost">
            </div>
            <div class="col-md-2">
              <label class="form-label" style="color: transparent">&nbsp</label>
              <button class="d-block w-100 btn btn-primary text-light" @click.prevent="makeOrder">order</button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
  <!--  <div class="card shadow-none border-0 mb-5 w-100 py-4 px-3 d-none" style="background-color: rgba(0,0,0,0.4);">-->
  <!--    <div class="card-body">-->
  <!--      <form action="">-->
  <!--        <div class="row">-->
  <!--          <div class="col-md-5">-->
  <!--            <label for="date" class="form-label">delivery date</label>-->
  <!--            <input type=text id="date" class="form-control" value="">-->
  <!--          </div>-->
  <!--          <div class="col-md-5">-->
  <!--            <label for="cost" class="form-label">estimated cost</label>-->
  <!--            <input type=text id="cost" class="form-control" v-model="cost">-->
  <!--          </div>-->
  <!--          <div class="col-md-2">-->
  <!--            <label class="form-label" style="color: transparent">&nbsp</label>-->
  <!--            <button class="d-block w-100 btn btn-primary text-light" @click.prevent="makeOrder">order</button>-->
  <!--          </div>-->
  <!--        </div>-->
  <!--      </form>-->
  <!--    </div>-->
  <!--  </div>-->

</template>

<script>
import {onMounted, ref} from "vue";
import DropZone from "@/components/DropZone";

import {SelectBase, SelectMulti, Cascader, CascaderMulti} from '@livelybone/vue-select';
// import 'node_modules/@livelybone/vue-select/lib/css/index.css'
import vueSelect from "@/components/VueSelect";
import vueMultiSelect from "@/components/VueMultiSelect";

export default {
  name: 'Form',
  components: {DropZone ,vueSelect, vueMultiSelect},
  setup() {
    const typeSelected = ref(false);
    const defaultPopperProps = {
      arrowPosition: 'start',
      arrowOffsetScaling: 1,
      popperOptions: {
        placement: 'bottom-start',
        // If component is Cascader or CascaderMulti -> `positionFixed: true`
        // More options in https://popper.js.org
      },
    };
    const checkFromTo = (type) => {
      let from = document.querySelector('#from').value;
      let to = document.querySelector('#to').value;
      type === 'to'
          ? (
              from === to
                  ? document.querySelector('#from').value = '' :
                  (
                      // document.querySelector('.d-none').classList.remove('d-none'),
                      document.querySelector('#from_' + to).classList.add('d-none'))
          )
          : (
              from === to
                  ? document.querySelector('#to').value = '' :
                  (
                      // document.querySelector('.d-none').classList.remove('d-none'),
                      document.querySelector('#to_' + from).classList.add('d-none'))
          )
      ;
      estimate();
    };

    const cost = ref(0);
    const typeIsText = ref(false);
    const estimate = () => {

      cost.value = document.querySelector('#count').value *
          document.querySelector('#service').options[document.querySelector('#service').selectedIndex].getAttribute('data-price') *
          // document.querySelector('#type').options[document.querySelector('#type').selectedIndex].getAttribute('data-price') *
          document.querySelector('#subject').options[document.querySelector('#subject').selectedIndex].getAttribute('data-price') *
          document.querySelector('#to').options[document.querySelector('#to').selectedIndex].getAttribute('data-price')
      ;
    };
    const selectType = (Type) => {
      Type === 'text' ?
          (
              // document.querySelector('#file').classList.add('d-none'),
              document.querySelector('#selectSection').classList.add('animate__zoomOut'),
                  setTimeout(() => {
                    typeSelected.value = true,
                        typeIsText.value = true,
                        document.querySelector('#textSection').classList.remove('animate__zoomOut'),
                        document.querySelector('#textSection').classList.add('animate__zoomIn'),
                        typeIsText.value = true
                  }, 200)
          )
          :
          (
              document.querySelector('#selectSection').classList.add('animate__zoomOut'),

                  setTimeout(() => {
                    typeSelected.value = true,
                        typeIsText.value = false,
                        document.querySelector('#fileSection').classList.remove('animate__zoomOut'),
                        document.querySelector('#fileSection').classList.add('animate__zoomIn')
                  }, 200)
          )
      ;
    }
    const txtFileToggle = () => {
      document.querySelector('#text').value = '';
      document.querySelector('#count').value = 0;
      // document.querySelector('#dzFile').value = null;


      !typeIsText.value ?
          (
              // document.querySelector('#file').classList.add('d-none'),
              document.querySelector('#fileSection').classList.add('animate__zoomOut'),
                  setTimeout(() => {
                    document.querySelector('#textSection').classList.remove('animate__zoomOut'),
                        document.querySelector('#textSection').classList.add('animate__zoomIn'),
                        typeIsText.value = true
                  }, 200)
          )

          :
          (
              document.querySelector('#textSection').classList.add('animate__zoomOut'),
                  setTimeout(() => {
                    document.querySelector('#fileSection').classList.remove('animate__zoomOut'),
                        document.querySelector('#fileSection').classList.add('animate__zoomIn'),
                        typeIsText.value = false
                  }, 200)
          )
      ;
    }
    const makeOrder = () => {

    };
    const countText = () => {
      let text = document.querySelector('#text').value;
      text = text.replaceAll('\n', ' ');
      text = text.split(' ')
      text = text.filter((el) => {
        return el !== ''
      });
      console.log(text);
      document.querySelector('#count').value = text.length;
    };

    const countFile = () => {

    };
    const translates = ref([]);
    const getTranslates = ()=>{
      axios.get('https://panel.tarjomeh1.webagent.ir/api/translate/language?to_id='+ document.querySelector('#siteLanguage').value)
          .then((response)=>{
           translates.value = response.data;
           console.log(translates.value);
          }).catch((error)=>{ console.error(error)})
    };
    onMounted(() => {
      getTranslates();
      estimate();
      document.querySelector('#siteLanguage').addEventListener('change', () => {
        getTranslates();
      });
    })

    // const showForm = (type) => {
    //   typeIsText.value = type === 'text';
    //
    //   document.querySelector('#selectType').classList.add('animate__zoomOut')
    //
    //   setTimeout(() => {
    //     // document.querySelector('#selectType').remove();
    //
    //     document.querySelector('#selectType').classList.remove('animate__zoomOut');
    //     document.querySelector('#selectType').classList.add('d-none')
    //
    //
    //     typeIsText ? (
    //             setTimeout(() => {
    //               typeSelected.value = true,
    //                   document.querySelector('#textSection').classList.add('zoomIn'),
    //                   document.querySelector('#textSection').classList.remove('d-none')
    //             }, 200)
    //         ) :
    //         (
    //             setTimeout(() => {
    //               typeSelected.value = true,
    //
    //                   document.querySelector('#fileSection').classList.add('zoomIn'),
    //                   document.querySelector('#fileSection').classList.remove('d-none')
    //             }, 200)
    //         );
    //   }, 200)
    //
    //   setTimeout(async () => {
    //     await document.querySelector('#selectSection').classList.add('d-none')
    //
    //
    //   }, 200);
    // }

    return {defaultPopperProps,
      checkFromTo, cost, estimate, makeOrder, countText, countFile, typeIsText,translates,
      // showForm,
      txtFileToggle, typeSelected, selectType, getTranslates
    }
  }
}
</script>

<style scoped>
label {
  cursor: pointer;
  margin-top: 10px;
}

.btn-select {
  height: 38px;
  font-size: 18px !important;
}

.or {
  font-size: 20px;

  line-height: 50px;
}

@media (min-width: 768px) {
  .btn-select {
    height: 150px;
    font-size: 25px !important;
    margin-top: 25px;
    margin-bottom: 25px;
  }

  /*}*/
  /*@media(min-width: 768px) {*/
  .or {
    line-height: 200px;
    font-size: 25px;

  }

}

button {
  cursor: pointer;
}

select option:checked,
select option:hover {
  box-shadow: 0 0 10px 100px #ffc107 inset;
}
/*Checked option item works in Chrome:*/

select:focus > option:checked {
  background: #ffc107 !important;
}
option:hover {
  background-color: yellow !important;
}
</style>