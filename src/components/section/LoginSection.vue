<template>
    <section class="login-section section-space-b pt-4 pt-md-5 mt-md-3">
        <div class="container">
                <div class="row align-items-center justify-content-center">
                    <div class="col-lg-6 mb-5 mb-lg-0 d-none d-lg-block">
                        <img :src="SectionData.loginData.img" alt="" class="img-fluid">
                    </div><!-- end col-lg-6 -->
                    <div class="col-lg-6">
                        <div class="section-head-sm">
                            <h2 class="mb-1">{{ SectionData.loginData.title }}</h2>
                            <p>{{ SectionData.loginData.subTitle }}</p>
                        </div>
                        <form action="#">
                            <div class="form-floating mb-4">
                                <input v-model="email" type="email" class="form-control" id="emailAddress" placeholder="name@example.com">
                                <label for="emailAddress">Addresse email</label>
                            </div><!-- end form-floating -->
                            <div class="form-floating mb-4">
                                <input v-model="password" type="password" class="form-control password" id="password" placeholder="Password">
                                <label for="password">Mot de passe</label>
                                <a href="password" class="password-toggle" title="Toggle show/hide pasword">
                                    <em class="password-shown ni ni-eye-off"></em>
                                    <em class="password-hidden ni ni-eye"></em>
                                </a>
                            </div><!-- end form-floating -->
                            <div class="d-flex flex-wrap align-items-center justify-content-between mb-4">
                                <router-link to="login" class="btn-link form-forget-password">Mot de passe oublié</router-link>
                            </div>
                            <button @click.prevent="login()" class="btn btn-primary w-100" >{{ SectionData.loginData.btnText }}</button>
                            <span class="d-block my-4">— ou se connecter avec —</span>
                           <ul class="btns-group d-flex">
                                <li class="text-center flex-grow-1"> 
                                            <button @click.prevent="loginGoogle()" class="btn bg-red-100 text-red g-btn"><em class="ni ni-google"></em> Google</button>
                                         <!--    <button @click.prevent="authProvider('facebook')" class="btn bg-blue-100 text-blue f-btn mx-3"><em class="ni ni-facebook"></em>Facebook</button> -->
                                </li>
                        
                            </ul>
                            <p class="mt-3 form-text">{{ SectionData.loginData.haveAccountText }} <router-link :to="SectionData.loginData.btnTextLink" class="btn-link">{{ SectionData.loginData.btnTextTwo }}</router-link></p>
                        </form>
                    </div><!-- end col-lg-6 -->
                </div><!-- end row -->
            </div><!-- end container -->
    </section>
</template>
<script>
// Import component data. You can change the data in the store to reflect in all component
import SectionData from '@/store/store.js'
import axios from 'axios'

export default {
  name: 'LoginSection',
  data () {
    return {
      SectionData,
      email:'',
      password:'',
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

  methods: {
      login(){
          console.log(this.email, this.password);
          const data = {
              email: this.email,
              password: this.password,
          }

          axios.post('auth/login',data)
            .then(
                response => {
                    console.log(response);
                 this.$router.push("/");
                }
            ).catch(
                error => {
                    console.log(error);
                }
            )
            
      },
       async loginGoogle(){
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