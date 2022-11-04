<template>
  <div
      @dragenter.prevent="toggleActive"
      @dragleave.prevent="toggleActive"
      @dragover.prevent
      @drop.prevent="drop($event)"
      :class="{'active-dropzone' : active}"
      class="pt-5 drop-zone w-100 text-primary rounded"><!--      @click="dropzoneClick"-->

    <span class="d-block" v-if="!dropzoneFile  && !dropzoneFileError && !loading"><i
        class="bi bi-cloud-upload"></i></span>
    <span class="d-block" v-if="!dropzoneFile && !dropzoneFileError && !loading">drag file and drop here</span>
    <span class="d-block  text-success" v-if="dropzoneFile && !dropzoneFileError && !loading"><i
        class="bi bi-file-earmark-check-fill"></i></span>
    <span class="d-block text-success" v-if="dropzoneFile && !dropzoneFileError && !loading">file uploaded!</span>

    <span class="d-block  text-danger" v-if="dropzoneFileError && !loading"><i
        class="bi bi-file-earmark-excel-fill"></i>
    </span>
    <span class="d-block text-danger" v-if="dropzoneFileError && !loading">file type error!</span>

    <span v-if="loading"><loader/></span>
    <br>


    <label id="label" class="rounded btn btn-primary " for="dzFile">choose file</label><br>
    <input type="file" id="dzFile" @change="selectedFile($event)" class="dzFile">


  </div>
  <div class="d-none">
    <img id="img" :src="dropzoneFile" style="width: 200px; height: auto" alt="">
  </div>
</template>

<script>
import {onMounted, ref} from "vue";
import Loader from "@/components/Loader";
export default {
  name: 'dropZone',
  components: {Loader},
  setup() {
    const dropzoneFileError = ref(false);
    const loading = ref(false);
    const dropzoneFile = ref('');
    const active = ref(false);
    const toggleActive = () => {
      active.value = !active.value;
    };
    const drop = (e) => {
      toggleActive();
      loading.value = true;
      var file = e.dataTransfer.files[0];
      if (file.type !== 'image/jpeg'
          && file.type !== 'image/png'
          && file.type !== 'application/pdf'
          && file.type !== 'application/vnd.openxmlformats-officedocument.wordprocessingml.document'
          && file.type !== 'application/msword'
          && file.type !== 'text/plain'
      ) {
        dropzoneFile.value = '';
        dropzoneFileError.value = true;

      } else {

        let formData = new FormData();
        if (e.dataTransfer.items) {
          formData.append('file', [...e.dataTransfer.items][0].getAsFile())
          // Use DataTransferItemList interface to access the file(s)
          // [...e.dataTransfer.items].forEach((item, i) => {
          //   // If dropped items aren't files, reject them
          //   if (item.kind === 'file') {
          //     const file = item.getAsFile();
          //     console.log(`… file[${i}] = ${file}`);
          //   }
          // }
          // );
        } else {
          // Use DataTransfer interface to access the file(s)
          formData.append('file', [...e.dataTransfer.items][0])

          // [...e.dataTransfer.files].forEach((file, i) => {
          //   console.log(`… file[${i}] = ${file}`);
          // });
        }


        uploadFile(formData)

      }



    };
    const selectedFile = (e) => {
      loading.value = true;
      dropzoneFileError.value = false;

      var file = document.querySelector('.dzFile').files[0];

      if (file.type !== 'image/jpeg'
          && file.type !== 'image/png'
          && file.type !== 'application/pdf'
          && file.type !== 'application/vnd.openxmlformats-officedocument.wordprocessingml.document'
          && file.type !== 'application/msword'
          && file.type !== 'text/plain'
      ) {

        dropzoneFile.value = '';
        dropzoneFileError.value = true;

      } else {
        if(file.type === 'application/pdf'){

          var img = new Image();

          // img.src = pdfCanvas().toDataURL();
          // alert(img.src);
          console.log('pdf');
        }
        let formData = new FormData();
        formData.append('file', document.querySelector('#dzFile').files[0])
        uploadFile(formData)
        dropzoneFileError.value = false;

        var reader = new FileReader();
        reader.onloadend = function () {

          dropzoneFile.value = reader.result;
        }
        reader.readAsDataURL(file);
      }


      setTimeout(() => {
        loading.value = false;

      }, 500)


    };
    const dropzoneClick = () => {
      document.querySelector('#label').click()
    };
    const uploadFile = (file) => {

      // axios.post('https://panel.tarjomeh1.webagent.ir/api/upload/file', file)
      axios.post('http://127.0.0.1:8000/api/upload/file', file)
          .then((response) => {
            console.log(response);
            setTimeout(() => {
              loading.value = false;
              dropzoneFileError.value = false;
            }, 500)

          })
          .catch((error) => {
            console.log(error)
          })


    };
    const plugin = document.createElement("script");

    onMounted(() => {
      document.querySelector('#changeToText').addEventListener('click', () => {
        dropzoneFile.value = '';
        dropzoneFileError.value = false;
        loading.value = false;

          plugin.setAttribute(
              "src",
              "https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.min.js"
          );
          plugin.async = true;
          document.head.appendChild(plugin);

      })
    })
    return {
      active, toggleActive, dropzoneFile, drop, selectedFile, dropzoneFileError,
      dropzoneClick, loading, uploadFile, plugin
    }
  }
}
</script>
<style scoped>
.drop-zone {
  width: 100px;
  height: 200px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  margin: 0px auto;
  /*border: 2px dashed #41b883;*/
  border: 3px dashed #ffc107;
  background-color: #fff;
  transition: .3s ease all;
  cursor: pointer;
  padding-top: 10px;
}

label {
  padding: 8px 12px;
  color: #fff;
  /*background-color: #ffc107;*/
  transition: .3s ease all;
  cursor: pointer;

}

.active-dropzone {
  color: #fff;
  border-color: #fff;
  background-color: #ffc107;
}

.active-dropzone label {
  background-color: #ffc107;
  /*border-color: #fff;*/
  color: #ffc107;
}

input {
  display: none;
}

.bi {
  font-size: 30px;
}
</style>