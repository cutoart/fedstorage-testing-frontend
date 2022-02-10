<template>
  <!-- Slider ============================================= -->
  <section id="slider" class="slider-img">
    <div
      id="carouselsliderIndicators"
      class="carousel slide"
      data-ride="carousel"
    >
      <div class="carousel-inner">
      <div v-if="commentIndex < items.length">
        <div
          class="carousel-item"
          :class="{ active: i == 0 }"
          v-for="(commentIndex,i) in commentsToShow"
              v-bind:key="commentIndex._id"
        >
          <div class="image-wrapper">
            <img
                :src="
                  $store.state.apiURL +
                  '/promotion/' +
                  items[commentIndex - 1].image
                "
                class="banner-image"
              />
          </div>
        </div>
        <a
          class="carousel-control-prev"
          href="#carouselsliderIndicators"
          role="button"
          data-slide="prev"
        >
          <span class="arrows" aria-hidden="true"
            ><i class="bx bx-chevron-left"></i
          ></span>
          <span class="sr-only">Previous</span>
        </a>
        <a
          class="carousel-control-next"
          href="#carouselsliderIndicators"
          role="button"
          data-slide="next"
        >
          <span class="arrows" aria-hidden="true"
            ><i class="bx bx-chevron-right"></i
          ></span>
          <span class="sr-only">Next</span>
        </a>
      </div>
       </div>
    </div>
  </section>
</template>

<script>
import APIService from "@/services/api.service.js";
import Store from "@/store/index";

export default {
  data() {
    return {
       items: [],
      commentsToShow: 0,
      totalComments: 0,
      commentIndex: 0,
      ShowContactusModal: false,
      ContactusModalContent: "",
    };
  },
  created() {
    document.title = this.$store.state.projecttitle + " - Promotion";
    Store.commit("showLoader");
    APIService.post("/ListOfPromotion", { usertype: "user" }, null).then(
      (response) => {
        Store.commit("hideLoader");
        response.data = response.data.filter(
          (x) => x.language == this.$store.state.language
        );
        this.$set(this, "items", response.data);
        this.totalComments = response.data.length;
        if (this.totalComments > 6) {
          this.commentsToShow = 6;
        } else {
          this.commentsToShow = this.totalComments;
        }
      }
    );
  },
    methods: {
    showComments() {
      this.commentsToShow + 6 > this.totalComments
        ? (this.commentsToShow = this.totalComments)
        : (this.commentsToShow += 6);
    },
  },
};
</script>

<style>
.banner-image {
  height: 600px !important;
}
.image-wrapper {
  height: 700px;
}
@media only screen and (max-width: 768px) {
  .banner-image {
    height: 400px !important;
  }
  .image-wrapper {
    height: 450px;
    margin-bottom: 20px;
  }
}
@media only screen and (max-width: 425px) {
  .banner-image {
    height: 250px !important;
  }
  .image-wrapper {
    height: 300px;  
  }
}
</style>
