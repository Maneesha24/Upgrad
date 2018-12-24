<template>
  <div class="card" style="width: 35rem;" id="addModal">
    <div class="card-header d-flex justify-content-between">
      <div>Add user</div>
    </div>
    <div class="card-content mt-3 mr-5 pb-3">
      <form action @submit="handleSubmit">
        <div class="input-group mb-3 ml-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon1">
              <i class="fas fa-fingerprint"></i>
            </span>
          </div>
          <input
            type="text"
            placeholder="Enter Employee ID"
            name="employeeID"
            class="form-control"
            v-model="user.id"
            required
          >
        </div>

        <div class="input-group mb-3 ml-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon1">
              <i class="fas fa-signature"></i>
            </span>
          </div>
          <input
            type="text"
            placeholder="Enter first name"
            class="form-control"
            name="firstName"
            v-model="user.firstName"
            required
          >
        </div>
        <div class="input-group mb-3 ml-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon1">
              <i class="fas fa-file-signature"></i>
            </span>
          </div>
          <input
            type="text"
            placeholder="Enter last name"
            name="lastName"
            class="form-control"
            v-model="user.lastName"
            required
          >
        </div>
        <div class="input-group mb-3 ml-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon1">
              <i class="fas fa-envelope"></i>
            </span>
          </div>
          <input
            type="text"
            placeholder="Enter email"
            id="email"
            name="email"
            class="form-control form-control-warning"
            v-model="user.email"
            required
          >
        </div>

        <div class="input-group mb-3 ml-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon1">
              <i class="fas fa-phone"></i>
            </span>
          </div>
          <input
            type="text"
            placeholder="Enter mobile number"
            name="number"
            class="form-control"
            v-model="user.phone"
            required
          >
        </div>

        <div class="input-group mb-3 ml-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon1">
              <i class="fas fa-battery-three-quarters"></i>
            </span>
          </div>
          <select class="custom-select" v-model="user.status" required>
            <option selected value="active">Active</option>
            <option value="inactive">Inactive</option>
          </select>
        </div>
        <div class="text-right">
          <button type="button" class="btn btn-secondary" @click="dismiss">Close</button>
          <button class="btn btn-primary ml-3">Save user</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "activeUser",
  data() {
    return {
      user: {
        id: "",
        firstName: "",
        lastName: "",
        email: "",
        phone: "",
        status: "active"
      }
    };
  },
  methods: {
    handleSubmit(event) {
      event.preventDefault();
      this.$emit("userData", this.user);
      this.user.id = "";
      this.user.firstName = "";
      this.user.lastName = "";
      this.user.email = "";
      this.user.phone = "";
    },
    dismiss() {
      document.getElementById("addModal").style.display = "none";
      this.$emit("close", true);
    }
  }
};
</script>

<style scoped>
</style>

