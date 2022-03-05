<template>
  <div>
    <div class="container">
      <br /><br />
      <ul class="steps">
        <li
          v-for="tab in tabs"
          :class="{ 'is-active': tab.selected }"
          v-bind:key="tab.name"
        >
          <div class="steps-content">
            <p class="is-size-4">{{ tab.name }}</p>
            <p class="digi">{{ tab.info }}</p>
          </div>
        </li>
      </ul>
      <br /><br />
    </div>
    <br />
    <div class="container form">
      <table class="table table-striped">
        <thead>
          <tr>
            <th>Size</th>
            <th>Area(Feet)</th>
            <th>Price</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in items" v-bind:key="index">
            <td>{{ item.size }}</td>
            <td>{{ item.areaFrom }} > {{ item.areaTo }}</td>
            <td>{{ item.price }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <br />
    <form @submit.prevent="handleSubmit">
      <div class="container form">
        <div class="row border-dark">
          <div
            class="sectoin-title ml-3"
            style="
              float: left;
              font-size: 24px;
              font-weight: 400 !important;
              margin-top: 10px;
            "
          >
            <strong>Moving Application</strong>
          </div>
          <div class="col-12 mt-3 form-group">
            <input
              class="form-control"
              type="number"
              v-model="moving.area"
              @change="estimatePrice"
              placeholder="Area"
              required
              
            />

             <input
              class="form-control"
              type="text"
              v-model="estimatedPriceInWords"
              placeholder="Estimated Price (HKD) "
              :readonly="true"
            />
             <input
              class="form-control"
              type="text"
              v-model="this.moving.estimatedPrice"
              placeholder="Estimated Price (HKD) "
              :hidden="true"
            />
          </div>
          
        
          <div class="col-12 mt-3 form-group">
            <input
              class="form-control"
              type="text"
              v-model="moving.name"
              placeholder="Name"
              required
            />
          </div>

          <div class="col-12 mt-3 form-group">
            <input
              class="form-control"
              type="number"
              v-model="moving.phone"
              placeholder="WhatsApp Number"
              required
            />
          </div>

          <div class="col-12 mt-3 form-group">
            <input
              class="form-control"
              type="email"
              v-model="moving.email"
              placeholder="Email"
            />
          </div>

          <div class="col-12 mt-3 form-group">
            <button type="submit" class="col-12 btn btn-send">Submit</button>
          </div>
        </div>
        <br /><br /><br /><br />
      </div>
    </form>
  </div>
</template>

<script>
import APIService from "@/services/api.service.js";
// import "bulma/css/bulma.css";
export default {
  name: "MovingServiceStep2b",
  data() {
    return {
      items: {},
      moving: {
        area: "",
        name: "",
        phone: "",
        email: "",
        estimatedPrice:"",
      },
        estimatedPriceInWords:"",
        estimatedPrice:"",

      tabs: [
        // {
        //   name: "Step 1",
        //   info: "Select",
        //   selected: false,
        // },
        {
          name: "Step 2-B",
          info: "Book",
          selected: true,
        },
        // {
        //   name: "Step 3",
        //   info: "Payment",
        //   selected: false,
        // },
      ],
    };
  },
  created() {
    APIService.post("/movingservicestep2", { usertype: "user" }, null).then(
      (response) => {
        this.$set(this, "items", response.data);
      }
     
    );
  },

  methods: {
    handleSubmit() {
      // this.$v.user.$touch();
      // if (this.$v.user.$invalid) {
      //   return;
      // }
      this.submitted = true;
      // this.user.apiurl = this.$store.state.apiURL;
      APIService.post("/moving-service-application", this.moving).then(() => {
        this.$successAlert("Apply Moving Service Successfully !.");
        this.$router.go();
        this.submitted = false;
      });
      this.submitted = true;
    },

    estimatePrice(){

      for(let i=0;i<this.items.length;i++){
      
      if(this.moving.area >=this.items[i].areaFrom && this.moving.area<=this.items[i].areaTo){
          // this.estimatedPrice =this.items[i].price;
          this.estimatedPriceInWords = "Estimated Price (HKD) : "+ this.items[i].price;
           this.estimatedPrice = this.items[i].price;
          this.moving.estimatedPrice =this.items[i].price;
           break
      }else{
        this.estimatedPrice ="Plese enter Area(feet) in number format !";
      
      }
        }
       
    }
  },
};
</script>

<style lang="scss">
.is-active .steps-content p {
  color: #4b5fc4 !important;
}
.steps-content p {
  color: #8fa7b3;
}
</style>

<style scoped>
.form {
  max-width: 700px;
}
.border-dark {
  border: 3px solid #dee2e6 !important;
}

.btn-send {
  background: #14b7eb;
  border-radius: 0px 0px 20px 0px;
  color: #ffffff;
}
</style>

<style>
.image {
  height: 50%;
  width: 100%;
}
.image1 {
  display: block;
  margin-left: auto;
  margin-right: auto;
  max-width: 250px;
}
.is-size-4 {
  font-size: 35px !important;
  margin: 8px !important;
  font-family: Roboto;
  font-style: normal;
  font-weight: bold;
}

.digi {
  font-size: 14px !important;
  margin: 20px !important;
  font-family: Roboto;
  font-style: normal;
  font-weight: bold;
  line-height: 16px;
}

ul li {
  display: block;
  /* position: relative; */
  /* float: left; */
  text-align: center;
}
</style>