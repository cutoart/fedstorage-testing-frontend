<template>
  <div>
        <div class="container">
       <div class="row">
         
         <div class="col-lg-4 col-md-6 col-sm-6"> 
           <div class="content-wrap">
                <div class="img-content">
           <img src="../../assets/images/movingservice/move1.jpg" max-width="300px"  max-height="300px"   style="object-fit: contain" />
           </div>
         </div>
         </div>
          <div class="col-lg-4 col-md-6 col-sm-6"> 
            <div class="content-wrap">
                <div class="img-content">
                  <img src="../../assets/images/movingservice/move2.jpg" max-width="300px"  max-height="300px"  style="object-fit: contain" />
                    </div>
         </div>
         </div>
          
             <div class="col-lg-4 col-md-6 col-sm-6"> 
            <div class="content-wrap">
                <div class="img-content">
              <img src="../../assets/images/movingservice/move3.jpg" max-width="300px"  max-height="300px" style="object-fit: contain" /></div>
             </div>
             </div>
             </div>
            </div>

                <div class="container  justify-content-center">
       <div class="row">

         <div class="col-lg-3 col-md-4 col-sm-6"> 
            <div class="content-wrap">
                <div class="img-content">
              <img src="../../assets/images/movingservice/move4.png" class="image" />
             </div>
             </div>
         </div>

          <div class="col-lg-3 col-md-4 col-sm-6"> 
             <div class="content-wrap">
                <div class="img-content">
              <img src="../../assets/images/movingservice/move5.png" class="image"/>
             </div>
             </div>
          </div>
           <div class="col-lg-3 col-md-4 col-sm-6">  
             <div class="content-wrap">
                <div class="img-content">
              <img src="../../assets/images/movingservice/move6.png" class="image" />
             </div>
             </div>
             </div>

            <div class="col-lg-3 col-md-4 col-sm-6"> 
               <div class="content-wrap">
                <div class="img-content">
              <img src="../../assets/images/movingservice/move7.png" class="image" />
             </div>
             </div>
            </div>
            
            </div>
       </div>
<div class="container form">
               <table class="table table-striped ">
              <thead>
                <tr>
                  <th>Size</th> 
                    <th>Area</th>
                    <th>Price</th>
                    </tr>
              </thead>
            <tbody>
               <tr  v-for="(item, index) in items"
                  v-bind:key="index">
                  <td>{{item.size}}</td>
                   <td>{{item.area}}</td>
                    <td>{{item.price}}</td>
                   </tr>
               
                
              </tbody>
            </table>
        </div>

         <form @submit.prevent="handleSubmit">
           <div class="container form">
<div class="row border-dark">
     <div
                  class="sectoin-title ml-3"
                  style="
                    float: left;
                    font-size: 24px;
                    font-weight: 400 !important;
                    margin-top :10px;
                  "
                >
                  <strong>Moving Application</strong>
                </div>
  <div class="col-12 mt-3 form-group">
   <input  class="form-control" type="text" v-model="moving.area" placeholder="Area">
    </div>
    
     <div class="col-12 mt-3 form-group">
    <input  class="form-control"  type="text" v-model="moving.name" placeholder="Name">
     </div>


      <div class="col-12 mt-3 form-group">
   <input  class="form-control" type="text" v-model="moving.phone" placeholder="WhatsApp Number">
  </div>

      <div class="col-12 mt-3 form-group">
    <input  class="form-control" type="email" v-model="moving.email" placeholder="Email">
     </div>

     <div class="col-12 mt-3 form-group">
    <button type="submit"  class="col-12 btn btn-send">Submit</button>
      </div>

</div>
</div>
  </form>
      </div> 
</template>

<script>
import APIService from "@/services/api.service.js";

export default {
  name: "MovingService",
data(){
  return {
    items: {},
      moving: {
        area: '',
        name: '',
        phone: '',
        email: '',
      },   
};
},
  created() {
    APIService.post("/movingservicestep2", { usertype: "user" }, null).then(
      (response) => {
        this.$set(this, "items", response.data);
      }
    );
  },

  methods:{
    handleSubmit() {
      // this.$v.user.$touch();
      // if (this.$v.user.$invalid) {
      //   return;
      // }
      this.submitted = true;
      // this.user.apiurl = this.$store.state.apiURL;
      APIService.post("/moving-service-application",this.moving).then(() => {
        this.$successAlert("Apply Moving Service Successfully !.");
        this.$router.go();
        this.submitted = false;
      });
      this.submitted = true;
    },

  }
}
</script>

<style lang="scss" scoped>
.img-content{
  width: 250px;
  // height: 250px;
}
.form{
  max-width: 700px;
}
.border-dark {
  border: 3px solid #dee2e6 !important;
}
.container{
  padding-bottom: 50px;
}
.btn-send {
  background: #14b7eb;
  border-radius: 0px 0px 20px 0px;
  color: #ffffff;
}
</style>

<style>
.image {
  height:50%;
  width: 100%;
}
.container{
  text-align: center;
}



@media only screen and (max-width: 992px) {
}

@media only screen and (max-width: 768px) {
}
</style>