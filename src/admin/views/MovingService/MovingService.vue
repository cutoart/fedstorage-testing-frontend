<template>
  <div>
    <CCol>
      <CCard>
        <CForm @submit.prevent="handleSubmit">
          <CCardHeader>
            <strong v-if="id == undefined && id == null">Add Moving Service </strong>
            <strong v-if="id != undefined && id != null">Edit Moving Service </strong>
          </CCardHeader>
          <CCardBody>
            <CRow>
              <CCol sm="6">
                <CInput
                  label="Moving Service Area From (Feet)*"
                  placeholder="Enter Area From (Feet)"
                  :isValid="checkIfValid('areaFrom')"
                  :value.sync="$v.user.areaFrom.$model"
                  :maxlength="99"
                  invalidFeedback="Area From is Required"
                />
              </CCol>
                <CCol sm="6">
                <CInput
                  label="Moving Service Area To (Feet)*"
                  placeholder="Enter Area To (Feet)"
                  :isValid="checkIfValid('areaTo')"
                  :value.sync="$v.user.areaTo.$model"
                  :maxlength="99"
                  invalidFeedback="Area To is Required"
                />
              </CCol>
              <CCol sm="6">
                <CInput
                  label="Moving Service Size*"
                  placeholder="Enter Size"
                  :isValid="checkIfValid('size')"
                  :value.sync="$v.user.size.$model"
                  :maxlength="99"
                  invalidFeedback="Size is Required"
                />
              </CCol>
              <CCol sm="6">
                <CInput
                  label="Price*"
                  placeholder="Enter Price"
                  :isValid="checkIfValid('price')"
                  :value.sync="$v.user.price.$model"
                  :maxlength="99"
                  invalidFeedback="Price is Required"
                />
              </CCol>
            </CRow>
          </CCardBody>
          <CCardFooter>
            <CButton type="submit" class="mr-1" color="primary">Save</CButton>
            <CButton
              type="button"
              router-link
              :to="{ name: 'MovingServiceList' }"
              class="mr-1"
              color="secondary"
              >Cancel</CButton
            >
          </CCardFooter>
        </CForm>
      </CCard>
    </CCol>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";
import APIService from "@/services/api.service.js";
import Store from "@/store/index";

export default {
  name: "app",
  created() {
    if (this.id != undefined && this.id != null) {
      Store.commit("showLoader");
      document.title = this.$store.state.projecttitle + " - Edit Moving Service";
      APIService.getById("/getMovingService", this.id).then((response) => {
        Store.commit("hideLoader");
        this.$set(this, "user", response.data);
      });
    } else {
      document.title = this.$store.state.projecttitle + " - Add Moving Service";
    }
  },
  data() {
    return {
      id: this.$route.params.id,
      user: {
        size: "",
        areaFrom: "",
        areaTo: "",
        price: "",
        createdBy: this.$store.state.userInfo.userId,
      },
    };
  },
  validations: {
    user: {
      size: { required },
      areaFrom: { required },
      areaTo: { required },
      price: { required },
    },
  },
  methods: {
    checkIfValid(fieldName) {
      const field = this.$v.user[fieldName];
      if (!field.$dirty) {
        return null;
      }
      return !(field.$invalid || field.$model === "");
    },

    handleSubmit() {
      this.$v.$touch();
      if (this.$v.$invalid) {
        return;
      }
      this.submitted = true;
      if (this.id != undefined && this.id != null && this.id != "") {
        APIService.post("/updateMovingService", this.user, this.id).then(() => {
          this.$successAlert("Moving Service Updated Successfully!.");
          this.$router.push({ name: "MovingServiceList" });
          this.submitted = false;
        });
      } else {
        APIService.post("/addMovingService", this.user).then(() => {
          this.$successAlert("Moving Service Added Successfully!.");
          this.$router.push({ name: "MovingServiceList" });
          this.submitted = false;
        });
      }
      this.submitted = true;
    },
  },
};
</script>