<template>
   <nav  dir="ltr" class="animate__animated animate__fadeInDown navbar navbar-expand-lg navbar-light bg-light">
     <div class="container-fluid">
       <a class="navbar-brand" href="#"></a>
       <button class="btn btn-dark d-lg-none" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasScrolling" aria-controls="offcanvasScrolling" >
         <span class="bi bi-list"></span>
       </button>
       <div class="collapse navbar-collapse" id="navbarSupportedContent">
         <ul class="navbar-nav me-auto mb-2 mb-lg-0 " dir="ltr">
           <li class="nav-item px-3 ">
             <a class="nav-link active text-primary" aria-current="page" href="#">Home</a>
           </li>
           <li class="nav-item px-3">
             <a class="nav-link active" aria-current="page" href="#">Services</a>
           </li>
           <li class="nav-item px-3">
             <a class="nav-link active" aria-current="page" href="#">Pricing</a>
           </li>
           <li class="nav-item px-3">
             <a class="nav-link active" aria-current="page" href="#">Job Opportunities</a>
           </li>
           <li class="nav-item px-3">
             <a class="nav-link active" aria-current="page" href="#">Contact us</a>
           </li>

         </ul>
         <form class="d-flex text-center">
           <div class="col-auto">
             <label for="siteLanguage" class="col-form-label mx-3">Language</label>
           </div>
           <div class="col-auto">

             <select id="siteLanguage" class="form-select">
               <option v-for="item in languages" :key="item.id" :value="item.id" class=" text-center">{{ item.name }}</option>
             </select>
           </div>
         </form>

       </div>


     </div>
   </nav>
   <div class="offcanvas offcanvas-start bg-dark text-light" data-bs-scroll="true" data-bs-backdrop="false" tabindex="-1" id="offcanvasScrolling" aria-labelledby="offcanvasScrollingLabel">
     <div class="offcanvas-header d-flex justify-content-end">
       <button type="button" class="btn-close btn-close-white" data-bs-dismiss="offcanvas" aria-label="Close"></button>
     </div>
     <div class="offcanvas-body ps-0 pe-4">
       <router-link to="/" class="btn btn-block w-100 my-1 text-start ps-5" data-bs-dismiss="offcanvas" aria-label="Close"
                    :class="{'btn-primary rounded-0 rounded-end text-dark': this.$route.name === 'Home','btn-dark text-primary': this.$route.name !== 'Home'}"> Home</router-link>
       <router-link to="/services" class="btn btn-block w-100 my-1 text-start ps-5"  data-bs-dismiss="offcanvas" aria-label="Close"
                    :class="{'btn-primary rounded-0 rounded-end text-dark': this.$route.name === 'Services','btn-dark text-primary': this.$route.name !== 'Services'}"> Services</router-link>
       <router-link to="/jobs" class="btn btn-block w-100 my-1 text-start ps-5"  data-bs-dismiss="offcanvas" aria-label="Close"
                    :class="{'btn-primary rounded-0 rounded-end text-dark': this.$route.name === 'Pricing','btn-dark text-primary': this.$route.name !== 'Pricing'}"> Pricing</router-link>
       <router-link to="/pricing" class="btn btn-block w-100 my-1 text-start ps-5"  data-bs-dismiss="offcanvas" aria-label="Close"
                    :class="{'btn-primary rounded-0 rounded-end text-dark': this.$route.name === 'Jobs','btn-dark text-primary': this.$route.name !== 'Jobs'}"> Jobs</router-link>
       <router-link to="/contact" class="btn btn-block w-100 my-1 text-start ps-5"  data-bs-dismiss="offcanvas" aria-label="Close"
                    :class="{'btn-primary rounded-0 rounded-end text-dark': this.$route.name === 'Contact','btn-dark text-primary': this.$route.name !== 'Contact'}"> Contact</router-link>
     </div>
   </div>

</template>

<script>
import {onMounted, ref} from "vue";
import Form from "@/components/Form";
export default {
  name: "Menu",
  components: { Form,},
  setup(){
    const languages = ref([]);
    const translates = ref([]);
    const getLanguages = ()=>{
      axios.get('https://panel.tarjomeh1.webagent.ir/api/language')
      .then((response)=>{
        languages.value = response.data;
      }).catch((error)=>{ console.error(error)})
    }


    onMounted(()=>{
      getLanguages();
    })
    return{
      languages, getLanguages, translates
    }
  }
}
</script>

<style scoped>

</style>