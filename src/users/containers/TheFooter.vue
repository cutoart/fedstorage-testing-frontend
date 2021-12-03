<template>
  <div>
    <section class="chat-call-section">
      <div class="container">
        <div class="col-12 row footer-detail" style="margin-left:14px">
          <div class="col-lg-2 col-md-12 col-sm-12">
            <span
              ><i class="bx bxs-phone des1"></i
              ><a
                class="des"
                :href="
                  'tel:' + $store.state.resource.header.number.replace(' ', '')
                "
                >{{ $store.state.resource.header.number }}</a
              ></span
            >
          </div>

          <div class="col-lg-2 col-md-12 col-sm-12">
            <span
              ><i class="bx bxl-whatsapp des1"></i
              ><a
                class="des"
                :href="
                  'tel:' +
                  $store.state.resource.footer.whatsappnumber.replace(' ', '')
                "
                >{{ $store.state.resource.footer.whatsappnumber }}</a
              ></span
            >
          </div>

          <div class="col-lg-6 col-md-12 col-sm-12 footer-email">
            <span
              ><i class="bx bx-envelope des1"></i
              ><a class="des" href="mailto:support@fedstorage.com.hk">{{
                $store.state.resource.footer.email
              }}</a></span
            >
          </div>
          <div class="extra-bg col-lg-2 col-md-12" style="float: right"></div>
        </div>
      </div>
    </section>
    <footer class="footer">
      <div class="footer-top">
        <div class="container">
          <div class="row footer-area">

           
<div class="col-md-4" style="text-align: center">
          <div class="ori-content">
              <a class="footer-content" href="#">
                {{ $store.state.resource.footer.ourservices }}</a
              >
            
           
              <router-link :to="{ name: 'AboutUs' }" class="footer-content">
                {{ $store.state.resource.header.aboutus }}</router-link
              >
          
           
              <router-link :to="{ name: 'FAQ' }" class="footer-content">
                {{ $store.state.resource.header.faq }}</router-link
              >
          </div>
               <div class="img-logo col-md-4 mobile-logo" style="text-align: center">
              <router-link :to="{ name: 'Home' }"
                ><img
                  src="/assets/images/logo.png"
                  class="custom-logo"
                  alt=""
                  itemprop="logo"
                   style="height: 50px"
              /></router-link>
            </div>
            
  </div>
            <div class="img-logo col-md-4 ori-logo" style="text-align: center">
              <router-link :to="{ name: 'Home' }"
                ><img
                 src="/assets/images/logo.png"
                  class="custom-logo"
                  alt=""
                  itemprop="logo"
                   style="height: 50px"
              /></router-link>
            </div>

            

  <div class="col-md-4" style="text-align: center">
  <div class="mobile-content">
                 <a class="footer-content" href="#">
                {{ $store.state.resource.footer.ourservices }}</a
              >
            
           
              <router-link :to="{ name: 'AboutUs' }" class="footer-content">
                {{ $store.state.resource.header.aboutus }}</router-link
              >
          
           
              <router-link :to="{ name: 'FAQ' }" class="footer-content">
                {{ $store.state.resource.header.faq }}</router-link
              >
</div>
              <router-link :to="{ name: 'ContactUs' }" class="footer-content">
                {{ $store.state.resource.header.contactus }}</router-link
              >
            
           
              <a v-on:click="changelanguage()" class="footer-content">
                {{ $store.state.resource.footer.eng }}</a
              >
            
           
              <a
                class="footer-content"
                href="mailto:support@fedstorage.com.hk"
                >{{ $store.state.resource.footer.support }}</a
              >
            

  </div>
          </div>
        </div>
      </div>
      <div class="footer-middle">
        <div class="container">
          <div class="footer-middle-content">
            <div class="social-links col-md-12">
              <ul>
                <li class="facebook">
                  <a
                    href="https://www.facebook.com/fedstoragehk"
                    target="_blank"
                    class="facebook"
                    ><span><i class="bx bxl-facebook"></i></span
                  ></a>
                </li>
                <li>
                  <a href="#" class="instagram"
                    ><span><i class="bx bxl-instagram"></i></span
                  ></a>
                </li>
                <li class="wechat">
                  <a href="#"
                    ><span><!-- <img src="images/wechat.png"> --></span></a
                  >
                </li>
                <!-- <li><a href="#"><span><i class='bx bxl-linkedin' ></i></span></a></li> -->
              </ul>
            </div>
          </div>
        </div>
      </div>
      <div class="footer-bottom">
        <div class="container">
          <p class="copyrights">
            © 2010 — {{ new Date().getFullYear() }}
            {{ $store.state.resource.footer.privacyterms }}
          </p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
import APIService from "@/services/api.service.js";
import Store from "@/store/index";

export default {
  methods: {
    changelanguage() {
      Store.commit(
        "setLanguage",
        this.$store.state.language == "chinese" ? "english" : "chinese"
      );
      APIService.post(
        "/GetLanguage",
        null,
        this.$store.state.language,
        false
      ).then(
        ((response) => {
          Store.commit("setResource", response.data);
        }).bind(this)
      );
    },
  },
};
</script>
<style scoped>
.des {
  color: #ffffff;
  font-size: 22px;
}
.des1 {
  color: #ffffff;
  padding-right: 10px;
  font-size: 20px;
  padding-top: 30px;
}
.footer-detail {
  height: 90px;
 /* margin-top: 9px; */
}
.footer-area {
  margin: 0;
  padding: 0;
  display: flex;
  margin-top: 35px;
  margin-left: 15px;
  justify-content: space-evenly;
}
.img-logo {
  margin-top: -10px;
}
.footer-content {
  color: #000000;
  font-weight: bold;
  font-size: 14px;
  padding: 15px;
}

.mobile-logo{
display: none;
}
.mobile-content{
display: none;
}

/* @media only screen and (max-width: 1024px) {
  .des{
    color: #ffffff;
    font-size: 21px !important;
  }
} */
@media only screen and (max-width: 992px) {
  .extra-bg {
    display: none;
  }
  .des {
    font-size: 19px;
  }
}

@media only screen and (max-width: 769px) {

.mobile-logo{
display: block;
}
.mobile-content{
display: block;
}

  .ori-logo{
display: none;
}
.ori-content{
display: none;
}


  .des {
    color: #ffffff !important;
    font-size: 15px;
  }
  .des1 {
    color: #ffffff;
    padding-right: 5px;
    font-size: 15px;
    padding-top: 0px;
  }
  .extra-bg {
    display: none;
  }
  .footer-detail a {
    font-size: 12px;
  }
  .footer-area {
    display: block;
  }
  .content-space {
    margin-top: 10px;
  }
  .img-logo {
    margin-top: 10px;
    margin-left: -10px;
  }
}

@media only screen and (min-width: 769px) and (max-width: 992px) {
  .footer-detail {
    height: auto;
  }
  .footer-email {
    padding-bottom: 30px;
  }
}

@media only screen and (min-width: 992px) and (max-width: 1045px)  {
  .des {
    font-size: 20px !important;
  }
}


</style>
