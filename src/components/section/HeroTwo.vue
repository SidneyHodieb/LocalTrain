<template>
    <div class="hero-wrap hero-wrap-2 section-space">
        <div class="container">
                    <div class="row align-items-center flex-md-row-reverse justify-content-between">
                        <div class="col-lg-5 col-sm-9 col-md-6">
                            <div class="hero-image">
                                <img :src="SectionData.heroDataTwo.img" alt="" class="w-100">
                            </div>
                        </div><!-- end col-lg-5 -->
                        <div class="col-lg-6 col-md-6">
                            <div class="hero-content pb-0 pt-md-0 pe-lg-4">
                                <h1 class="hero-title mb-4"><span class="underline--magical">Revendez</span> et <span class="underline--magical">Achetez</span>  des <span >billets de Train !</span> </h1>
                              
                                      <section class="hero-text mb-4 pb-1">
               
                    <div class="row align-items-center">

                        <div class="col-lg-6 col-md-4">
                             <div class="mb-3">
                                <label class="h4">Départ</label>
                    <input id="autocomplete" style="font-weight: 511;"  type="text" class="form-control form-control-s1" placeholder="Lyon">

                            </div>
                        </div><!-- end col -->
                        <div class="col-lg-6 col-md-4">
                             <div class="mb-3">
                                <label class="h4 text-primary">Arrivée</label>
                                <input id="autocomplete2" style="font-weight: 511;" type="text" class="form-control form-control-s1" placeholder="Lyon">
                            </div>
                        </div><!-- end col -->
                      
                    </div><!-- row -->
               
    </section>
                                    <!-- {{ SectionData.heroDataTwo.content }} -->
                                   
                                <!-- button group -->
                                <ButtonGroup :btns="SectionData.btnDataThree" classname="hero-btns"></ButtonGroup>
                            </div><!-- hero-content -->
                        </div><!-- col-lg-6 -->
                    </div><!-- end row -->
        </div><!-- .container-->
    </div><!-- end hero-wrap -->
</template>

<script>
// Import component data. You can change the data in the store to reflect in all component
import SectionData from '@/store/store.js'
/* import vSelect from 'vue-select' */


export default {

components: {
  /*   vSelect,          */   
},

  name: 'HeroTwo',
  data () {
    return {
      SectionData,
       options: [
      {
          title: 'Read the Docs',
          icon: 'fa-book',
          url: 'https://codeclimate.com/github/sagalbot/vue-select'
        },
        {
          title: 'Paris la belle',
          icon: 'fa-github',
          url: 'https://codeclimate.com/github/sagalbot/vue-select'
        },
        {
          title: 'View on NPM',
          icon: 'fa-database',
          url: 'https://codeclimate.com/github/sagalbot/vue-select'
        },
        {
          title: 'View Codepen Examples',
          icon: 'fa-pencil',
          url: 'https://codeclimate.com/github/sagalbot/vue-select'
        }
    ]
  
    }
  },

  mounted(){
    const google = window.google

    var autocomplete = new google.maps.places.Autocomplete(
 document.getElementById("autocomplete"),
 );
 autocomplete.setComponentRestrictions({ // restrict the country
 country: ["fr"]
 })

 var autocomplete2 = new google.maps.places.Autocomplete(
 document.getElementById("autocomplete2"),
 );
 autocomplete2.setComponentRestrictions({ // restrict the country
 country: ["fr"]
 })

  }

  
}
</script>

<style lang="scss">
.underline--magical {
  background-image: linear-gradient(120deg, #84fab0 0%, #8fd3f4 100%);
  background-repeat: no-repeat;
  background-size: 100% 0.2em;
  background-position: 0 88%;
  transition: background-size 0.25s ease-in;
  &:hover {
    background-size: 100% 88%;
  }
}
</style>