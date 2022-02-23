<template>
  <div>
    <CCard>
      <CCardHeader>
        <CRow>
          <CCol>
            <strong>Moving Service</strong>
          </CCol>
          <CCol col="2">
            <CButton block router-link :to="{ name: 'AddMovingService' }" color="dark"
              >Add Moving Service</CButton
            >
          </CCol>
        </CRow>
      </CCardHeader>
      <CCardBody>
        <CDataTable
          :hover="true"
          :striped="true"
          :border="true"
          :items="item"
          :fields="fields"
          :column-filter="true"
          :table-filter="true"
          :responsive="true"
          :items-per-page="20"
          :items-per-page-select="true"
          pagination
          sorter
        >
          <!-- <template #ChineseBranchName="{ item }">
            <td>
              {{
                item.ChineseBranchName != null &&
                item.ChineseBranchName != undefined &&
                item.ChineseBranchName != ""
                  ? item.ChineseBranchName
                  : "-"
              }}
            </td>
          </template> -->
          <template #status="{ item }">
            <td>
              <span>
                <CDropdown
                  size="sm"
                  toggler-text="Action"
                  color="link"
                  class="m-0 d-inline-block"
                >
                  <CDropdownItem
                    :to="{
                      name: 'EditMovingService',
                      params: { id: item._id },
                    }"
                    >Edit</CDropdownItem
                  >
                  <CDropdownItem
                    v-if="item.deleted == false"
                    @click="deActivateItem(item._id, item.deleted)"
                    >Deactivate</CDropdownItem
                  >
                  <CDropdownItem
                    v-else
                    @click="deActivateItem(item._id, item.deleted)"
                    >Activate</CDropdownItem
                  >
                  <CDropdownItem @click="deleteItem(item._id)"
                    >Delete</CDropdownItem
                  >
                </CDropdown></span
              >
            </td>
          </template>
        </CDataTable>
      </CCardBody>
    </CCard>
  </div>
</template>

<script>
import APIService from "@/services/api.service.js";
import Store from "@/store/index";
export default {
  name: "MovingService",
  data() {
    return {
      item: [],
      fields: [
        {
          key: "Size",
          label: "Size",
          sortable: true,
          sortDirection: "asc",
        },
        {
          key: "Area",
          label: "Area",
          sortable: true,
          sortDirection: "asc",
        },
        {
          key: "Price",
          label: "Price",
          sortable: true,
          sortDirection: "asc",
        },
        {
          key: "status",
          label: "Action",
          sortable: true,
          sortDirection: "asc",
          filter: false,
        },
      ],
      userId: this.$store.state.userInfo.userId,
    };
  },
  created() {
    Store.commit("showLoader");
    document.title = this.$store.state.projecttitle + " - Moving Service";
    this.getMovingServiceListData();
  },
  methods: {
    getMovingServiceListData() {
      APIService.post(
        "/movingservicelist",
        this.$store.state.userInfo.userType == "Users"
      ).then((response) => {
        Store.commit("hideLoader");
        this.$set(this, "item", response.data);
      });
    },
    deActivateItem(id, deleted) {
      var req = {
        id: id,
        userId: this.userId,
        deleted: deleted,
      };
      this.$confirm({
        message:
          "Are you sure your want to " +
          (deleted == false ? "Deactivate" : "Activate") +
          " this record?",
        button: {
          no: "No",
          yes: "Yes",
        },
        callback: (confirm) => {
          if (confirm) {
            APIService.delete("/DeActivateMovingService", req).then((response) => {
              this.$set(this, "item", response.data);
            });
          }
        },
      });
    },
    deleteItem(id) {
      var req = {
        id: id,
        userId: this.userId,
      };
      this.$confirm({
        message: "Are you sure your want to Delete this record?",
        button: {
          no: "No",
          yes: "Yes",
        },
        callback: (confirm) => {
          if (confirm) {
            APIService.delete("/DeleteMovingService", req).then((response) => {
              this.$set(this, "item", response.data);
            });
          }
        },
      });
    },
  },
};
</script>




