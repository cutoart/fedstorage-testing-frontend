<template>
  <div>
    <div class="container">
      <br><br>
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
     <br><br>
    </div> 

    <div class="container">
      <div class="row">
        <div class="col-lg-4 col-md-4 col-sm-6">
          <img
            src="../../assets/images/movingservice/move1.jpg"
            class="image1"
          />
        </div>

        <div class="col-lg-4 col-md-4 col-sm-6">
          <img
            src="../../assets/images/movingservice/move2.jpg"
            class="image1"
          />
        </div>

        <div class="col-lg-4 col-md-4 col-sm-6">
          <img
            src="../../assets/images/movingservice/move3.jpg"
            class="image1"
          />
        </div>
      </div>
    </div>
<br><br><br><br>
    <div class="container">
      <div class="row">
        <div class="col-lg-3 col-md-4 col-sm-6">
          <img
            src="../../assets/images/movingservice/move4.png"
            class="image1"
          />
        </div>

        <div class="col-lg-3 col-md-4 col-sm-6">
          <img
            src="../../assets/images/movingservice/move5.png"
            class="image1"
          />
        </div>

        <div class="col-lg-3 col-md-4 col-sm-6">
          <img
            src="../../assets/images/movingservice/move6.png"
            class="image1"
          />
        </div>

        <div class="col-lg-3 col-md-4 col-sm-6">
          <img
            src="../../assets/images/movingservice/move7.png"
            class="image1"
          />
        </div>
      </div>
        <br><br>
      <div class="btnNextDiv">
       <router-link :to="'/movingservicestep2b'" class="col-5 btn btn-next">Next</router-link>
       </div>
    </div>
   
    <br><br><br><br>
    </div>
 
</template>

<script>

export default {
data(){
  return{
     tabs: [
        // {
        //   name: "Step 1",
        //   info: "Select",
        //   selected: false,
        // },
        {
          name: "Step 2-A",
          info: "Book",
          selected: true,
        },
        // {
        //   name: "Step 3",
        //   info: "Payment",
        //   selected: false,
        // },
      ],
  }
}
};
</script>

 <style lang="scss">
.is-active .steps-content p {
  color: #4B5FC4 !important;
}
.steps-content p {
  color: #8fa7b3;
}
</style>

<style scoped>
.img-content {
  width: 250px;
  text-align: center;
}

.btn-next {
  background: #14b7eb;
  border-radius: 0px 0px 20px 0px;
  color: #ffffff;
}
</style>

<style>
.btnNextDiv{
  text-align: end;
}
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