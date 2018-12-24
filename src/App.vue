<template>
  <div id="app">
    <div class="landing container" id="main">
      <header class="row d-flex justify-content-center mt-4">
        <div class="col-md-3 text-right">
          <img
            src="https://ci6.googleusercontent.com/proxy/uPh3kp9eh0-YSNeguv9IKX71MGh40hdwIe-iImMQHQgiESxN3Ur6Z1Socgf2lR33ZuZORLHpoQ=s0-d-e1-ft#https://images.upgrad.com/upgrad.png"
            alt
          >
        </div>
        <div class="col-md-5">
          <h3>ASSIGNMENT</h3>
        </div>
      </header>

      <main class="row text-center mt-5 pl-3 mr-1">
        <div class="input-group mb-3">
          <input
            type="text"
            class="form-control"
            placeholder="Enter your search"
            aria-describedby="button-addon2"
            v-model="search"
          >
          <div class="input-group-append">
            <button
              class="btn btn-primary"
              type="button"
              id="button-addon2"
              @click="onSubmit"
            >Add User</button>
          </div>
        </div>
      </main>

      <section>
        <table>
          <thead>
            <tr>
              <th>Employee_Id</th>
              <th>First name</th>
              <th>Last name</th>
              <th>Email</th>
              <th>Phone</th>
              <th>Status</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="user in filteredUsers" :key="user.name">
              <td>{{user.id}}</td>
              <td>{{user.firstName}}</td>
              <td>{{user.lastName}}</td>
              <td>{{user.email}}</td>
              <td>{{user.phone}}</td>
              <td>
                <toggle-input :fullName="user.firstName" :status="user.status"></toggle-input>
              </td>
            </tr>
          </tbody>
        </table>
      </section>
    </div>
    <addUser v-show="show" id="addModal" @userData="onUserDataSubmit" @close="closeModalOnClick"/>
  </div>
</template>


<script>
import addUser from "./components/addUser.vue";
import toggleInput from "./components/toggleInput.vue";

export default {
  name: "App",
  components: {
    addUser,
    toggleInput
  },
  data() {
    return {
      show: false,
      showActiveModal: false,
      users: [],
      search: "",
      closeModal: ""
    };
  },
  mounted() {
    this.users.push({
      id: "1",
      firstName: "Maneesha",
      lastName: "venigalla",
      email: "venigallamaneesha24@gmail.com",
      phone: "9398231139",
      status: "active"
    },{
      id: "2",
      firstName: "John",
      lastName: "Doe",
      email: "john@doejohn.com",
      phone:"9393993933",
      status:"inactive"
    });
  },
  methods: {
    onSubmit() {
      this.show = !this.show;
      document.getElementById("main").style.opacity = "0.3";
    },
    onUserDataSubmit(value) {
      this.users.push({
        id: value.id,
        firstName: value.firstName,
        lastName: value.lastName,
        email: value.email,
        phone: value.phone
      });
      this.show = false;
      document.getElementById("main").style.opacity = "1";
    },
    closeModalOnClick() {
      this.show = !this.show;
      document.getElementById("main").style.opacity = "1";
    }
  },
  computed: {
    filteredUsers() {
      return this.users.filter(user => {
        return (
          user.email.toLowerCase().indexOf(this.search.toLowerCase()) > -1 ||
          user.firstName.indexOf(this.search.toLowerCase()) > -1 ||
          user.lastName.indexOf(this.search.toLowerCase()) > -1 ||
          user.id.indexOf(this.search.toLowerCase()) > -1 ||
          user.phone.indexOf(this.search.toLowerCase()) > -1
        );
      });
    }
  }
};
</script>

<style>
#addModal {
  position: absolute;
  top: 10%;
  left: 30%;
  z-index: 10;
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
}

table {
  width: 100%;
  max-width: 100%;
  margin-bottom: 1rem;
  background-color: transparent;
  border-collapse: collapse;
}

table thead th {
  border-top: none;
  border-bottom: none;
  font-weight: 600;
  text-transform: uppercase;
  vertical-align: bottom;
  font-size: 0.875rem;
  text-align: left;
}

table thead {
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14),
    0 3px 1px -2px rgba(0, 0, 0, 0.12), 0 1px 5px 0 rgba(0, 0, 0, 0.2);
}
table td,
table th {
  padding: 1rem;
  vertical-align: top;
  border-top: 1px solid #e4e7ed;
}

table tbody td {
  font-size: 1rem;
  padding-bottom: 0.9rem;
  padding-top: 1rem;
  text-align: left;
}
table tbody tr {
  padding-bottom: 1rem;
}
.j-table.table-striped tbody tr:nth-of-type(odd) {
  background-color: rgba(0, 0, 0, 0.02);
}
</style>

