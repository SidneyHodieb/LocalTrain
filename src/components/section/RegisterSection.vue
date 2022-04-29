<template>
    <section class="register-section section-space-b pt-4 pt-md-5 mt-md-3">
            <div class="container">
                <div class="row align-items-center justify-content-center">
                    <div class="col-lg-6 mb-lg-0 d-none d-lg-block">
                        <img :src="SectionData.registerData.img" alt="" class="img-fluid">
                    </div><!-- end col-lg-6 -->
                    <div class="col-lg-6 col-md-9">
                        <div class="section-head-sm">
                            <h2 class="mb-2" v-html=" SectionData.registerData.title"></h2>
                            <p>{{ SectionData.registerData.subTitle }}</p>
                        </div>
                        <form @submit.prevent="handleSubmit" action="#">
                            <div class="form-floating mb-4">
                                <input v-model="firstname" type="text" class="form-control" id="fullName" placeholder="Name">
                                <label for="fullName">Fisrt name</label>
                            </div><!-- end form-floating -->
                            <div class="form-floating mb-4">
                                <input  v-model="lastname" type="text" class="form-control" id="userName" placeholder="Username">
                                <label for="userName">Last name</label>
                            </div><!-- end form-floating -->
                            <div class="form-floating mb-4">
                                <input type="email"  v-model="email" class="form-control" id="emailAddress" placeholder="name@example.com">
                                <label for="emailAddress">Adresse email</label>
                            </div><!-- end form-floating -->
                            <div class="form-floating mb-4">
                                <input type="password"  v-model="password" class="form-control password" id="password" placeholder="Password">
                                <label for="password">Mot de lasse</label>
                                <a href="password" class="password-toggle" title="Toggle show/hide pasword">
                                    <em class="password-shown ni ni-eye-off"></em>
                                    <em class="password-hidden ni ni-eye"></em>
                                </a>
                            </div><!-- end form-floating -->
                            <p class="mb-4 form-text" >{{ SectionData.registerData.termText }}</p>
                            <button class="btn btn-primary w-100" type="submit">{{ SectionData.registerData.btnText }}</button>
                            <span class="d-block my-4">— ou  —</span>
                            <ul class="btns-group d-flex">
                                <li class="text-center flex-grow-1"> 
                                            <button @click.prevent="registerGoogle()" class="btn bg-red-100 text-red g-btn"><em class="ni ni-google"></em> Continuer avec Google</button>
                                         <!--    <button @click.prevent="authProvider('facebook')" class="btn bg-blue-100 text-blue f-btn mx-3"><em class="ni ni-facebook"></em>Facebook</button> -->
                                </li>
                        
                            </ul>
                            <p class="mt-3 form-text">{{ SectionData.registerData.haveAccountText }} <router-link :to="SectionData.registerData.btnTextLink" class="btn-link">{{ SectionData.registerData.btnTextTwo }}</router-link></p>
                        </form>
                    </div><!-- end col-lg-6 -->
                </div><!-- end row -->
            </div><!-- end container -->
        </section><!-- end register-section -->
</template>

<script>
// Import component data. You can change the data in the store to reflect in all component
import SectionData from '@/store/store.js'
import axios from 'axios'
export default {
  name: 'RegisterSection',
  data () {
    return {
      SectionData,
      email:'',
      password:'',
      firstname:'',
      lastname:'',
      isLogin: false,

    }
  },
  mounted () {
    /*  ======== Show/Hide passoword ======== */
    function showHidePassword(selector){
        let elem = document.querySelectorAll(selector);
        if(elem.length > 0){
            elem.forEach(item => {
            item.addEventListener("click", function(e){
                e.preventDefault();
                let target = document.getElementById(item.getAttribute("href"));
                if(target.type == "password") {
                target.type = "text";
                item.classList.add("is-shown");
                }else{
                target.type = "password";
                item.classList.remove("is-shown");
                }
            });

            });
        }
    }

    showHidePassword(".password-toggle");


  },

  methods:{
      handleSubmit(){
          const data = {
              firstname: this.firstname,
              lastname: this.lastname,
              email: this.email,
              password: this.password,
          }

          axios.post('auth/register',data)
            .then(
                response => {
                    console.log(response);
                }
            ).catch(
                error => {
                    console.log(error);
                }
            )
      },
      async logOut(){
          const result = this.$gAuth.signOut()
          console.log(`result`, result);
      },
      async registerGoogle(){
          const googleUser = await this.$gAuth.signIn()
          console.log("googleuser :", googleUser);
          console.log("getId : ",googleUser.getId());
          console.log("getAuthResponse", googleUser.getAuthResponse());
          console.log(
              "getAuthResponse$G",
              this.$gAuth.GoogleAuth.currentUser.get().getAuthResponse()
          );
          this.isLogin = this.$gAuth.isAuthorized;
      }

    
  }
}
</script>