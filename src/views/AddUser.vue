<template>
  <main>
    <div class="container-fluid">
      <div class="page-header min-height-300" style="
          background-image: url('https://images.unsplash.com/photo-1531512073830-ba890ca4eba2?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1920&q=80');
          margin-right: -24px;
          margin-left: -34%;
        ">
        <span class="mask bg-gradient-success opacity-6"></span>
      </div>
    </div>
    <div class="py-4 container-fluid">
      <div class="row">
        <div class="col">
          <div class="card">
            <div class="card-header pb-0">
              <div class="d-flex align-items-center">
                <p class="mb-0">Add Profile</p>
                <argon-button color="success" size="sm" class="ms-auto" @click="add">Create</argon-button>
              </div>
            </div>
            <div class="card-body">
              <p class="text-uppercase text-sm">User Information</p>
              <div class="row">
                <div class="col-md-12">
                  <label for="example-text-input" class="form-control-label">Email address</label>
                  <input class="form-control" type="email" v-model="email" />
                </div>
                <div class="col-md-6">
                  <label for="example-text-input" class="form-control-label">First name</label>
                  <input class="form-control" type="text" v-model="first_name" />
                </div>
                <div class="col-md-6">
                  <label for="example-text-input" class="form-control-label">Last name</label>
                  <input class="form-control" type="text" v-model="last_name" />
                </div>
              </div>
              <hr class="horizontal dark" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import ArgonInput from "@/components/ArgonInput.vue";
import ArgonButton from "@/components/ArgonButton.vue";
import axios from 'axios';

const body = document.getElementsByTagName("body")[0];

export default {
  name: "adduser",

  data() {
    return {
      showMenu: false,
      errors: [],
      email: '',
      first_name: '',
      last_name: ''
    };
  },

  methods: {
    add() {
      axios.post(`https://reqres.in/api/users`, {
        email: this.email,
        first_name: this.first_name,
        last_name: this.last_name
      })
        .then(response => {
          console.log(response)
          alert(response.status + " User created")
        })
        .catch(e => {
          this.errors.push(e)
        })
    }
  },

  components: { ArgonInput, ArgonButton },

  beforeMount() {
    this.$store.state.imageLayout = "profile-overview";
    this.$store.state.showNavbar = false;
    this.$store.state.showFooter = true;
    this.$store.state.hideConfigButton = true;
    body.classList.add("profile-overview");
  },
  beforeUnmount() {
    this.$store.state.isAbsolute = false;
    this.$store.state.imageLayout = "default";
    this.$store.state.showNavbar = true;
    this.$store.state.showFooter = true;
    this.$store.state.hideConfigButton = false;
    body.classList.remove("profile-overview");
  }
};
</script>
