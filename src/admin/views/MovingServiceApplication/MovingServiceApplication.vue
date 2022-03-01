<template>
  <div>
    <CCol>
      <CCard>
        <CForm @submit.prevent="handleSubmit">
          <CCardHeader>
            <strong v-if="id == undefined && id == null">Add Moving Service Application </strong>
            <strong v-if="id != undefined && id != null">Edit Moving Service Application </strong>
          </CCardHeader>
          <CCardBody>
            <CRow>
              <CCol sm="6">
                <CInput
                  label="Area*"
                  placeholder="Enter Area"
                  :isValid="checkIfValid('area')"
                  :value.sync="$v.user.area.$model"
                  :maxlength="99"
                  invalidFeedback="Area is Required"
                />
              </CCol>
              <CCol sm="6">
                <CInput
                  label="Name*"
                  placeholder="Enter Name"
                  :isValid="checkIfValid('name')"
                  :value.sync="$v.user.name.$model"
                  :maxlength="99"
                  invalidFeedback="Name is Required"
                />
              </CCol>
              <CCol sm="6">
                <CInput
                  label="Phone*"
                  placeholder="Enter WhatsApp Number"
                  :isValid="checkIfValid('phone')"
                  :value.sync="$v.user.phone.$model"
                  :maxlength="99"
                  invalidFeedback="Phone is Required"
                />
              </CCol>

              <CCol sm="6">
                <CInput
                  label="Email*"
                  placeholder="Enter Email"
                  :isValid="checkIfValid('email')"
                  :value.sync="$v.user.email.$model"
                  :maxlength="99"
                  invalidFeedback="Email is Required"
                />
              </CCol>

            </CRow>
          </CCardBody>
          <CCardFooter>
            <CButton type="submit" class="mr-1" color="primary">Save</CButton>
            <CButton
              type="button"
              router-link
              :to="{ name: 'MovingServiceApplicationList' }"
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
      document.title = this.$store.state.projecttitle + " - Edit Moving Service Application";
      APIService.getById("/getMovingServiceApplication", this.id).then((response) => {
        Store.commit("hideLoader");
        this.$set(this, "user", response.data);
      });
    } else {
      document.title = this.$store.state.projecttitle + " - Add Moving Service Application";
    }
  },
  data() {
    return {
      id: this.$route.params.id,
      user: {
        area: "",
        name: "",
        phone: "",
        email: "",
        createdBy: this.$store.state.userInfo.userId,
      },
    };
  },
  validations: {
    user: {
      area: { required },
      name: { required },
      phone: { required },
      email: { required },
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
        APIService.post("/updateMovingServiceApplication", this.user, this.id).then(() => {
          this.$successAlert("Moving Service Application Updated Successfully!.");
          this.$router.push({ name: "MovingServiceApplicationList" });
          this.submitted = false;
        });
      } else {
        APIService.post("/addMovingServiceApplication", this.user).then(() => {
          this.$successAlert("Moving Service Application Added Successfully!.");
          this.$router.push({ name: "MovingServiceApplicationList" });
          this.submitted = false;
        });
      }
      this.submitted = true;
    },
  },
};
</script>