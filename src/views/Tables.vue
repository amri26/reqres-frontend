<template>
  <div class="py-4 container-fluid">
    <div class=" row">
      <div class="col-12">
        <div class="card">
          <div class="card-header pb-0">
            <h6>Authors table</h6>
          </div>
          <div class="card-body px-0 pt-0 pb-2">
            <div class="table-responsive p-0">
              <table class="table align-items-center mb-0">
                <thead>
                  <tr>
                    <th class="text-uppercase text-secondary text-xxs font-weight-bolder opacity-7">Author</th>
                    <th class="text-uppercase text-secondary text-xxs font-weight-bolder opacity-7 ps-2">Email</th>
                    <th class="text-secondary opacity-7"></th>
                  </tr>
                </thead>
                <tbody v-if="posts && posts.length">
                  <tr v-for="p in posts">
                    <td>
                      <div class="d-flex px-2 py-1">
                        <div>
                          <img :src="p.avatar" class="avatar avatar-sm me-3" />
                        </div>
                        <div class="d-flex flex-column justify-content-center">
                          <h6 class="mb-0 text-sm">{{p.first_name}} {{p.last_name}}</h6>
                        </div>
                      </div>
                    </td>
                    <td>
                      <p class="text-xs font-weight-bold mb-0">{{p.email}}</p>
                    </td>
                    <td class="align-middle">
                      <div class="ms-auto text-end">
                        <a class="btn btn-link text-danger text-gradient px-3 mb-0" @click="remove">
                          <i class="far fa-trash-alt me-2" aria-hidden="true"></i>Delete
                        </a>
                        <a class="btn btn-link text-dark px-3 mb-0" href="Profile">
                          <i class="fas fa-pencil-alt text-dark me-2" aria-hidden="true"></i>Edit
                        </a>
                      </div>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "table",

  data() {
    return {
      posts: [],
      errors: []
    };
  },

  async created() {
    try {
      const response = await axios.get(`https://reqres.in/api/users?page=2`);
      this.posts = response.data.data;
    }
    catch (e) {
      this.errors.push(e);
    }
  },
  
  methods: {
    remove() {
      axios.delete(`https://reqres.in/api/users/2`)
        .then(response => {
          console.log(response);
          alert(response.status + " User deleted")
        })
        .catch(e => {
          this.errors.push(e);
        });
    }
  }
};
</script>
