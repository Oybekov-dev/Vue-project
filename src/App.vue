<script setup>
import HelloWorld from "./components/HelloWorld.vue";
</script>

<template>
  <div>
    <div class="app">
      <div class="container">
        <div id="row" class="d-flex gap-4">
          <div id="box1" class="w-50">
            <div class="alert alert-danger text-center" v-if="error">
              {{ errorAlert }}
            </div>
            <form>
              <div class="mb-3">
                <label for="name" class="form-label">Your name</label>
                <input
                  type="email"
                  class="form-control"
                  id="name"
                  aria-describedby="emailHelp"
                  v-model="name"
                />
              </div>
              <div class="mb-3">
                <label for="email" class="form-label">Email address</label>
                <input
                  type="email"
                  class="form-control"
                  id="email"
                  aria-describedby="emailHelp"
                  v-model="email"
                />
                <div id="emailHelp" class="form-text">
                  We'll never share your email with anyone else.
                </div>
              </div>
              <div class="mb-3">
                <label for="age" class="form-label">Age</label>
                <input
                  type="number"
                  class="form-control"
                  id="age"
                  v-model="age"
                />
              </div>
              <button type="button" class="btn btn-primary" @click="addUser">
                Add user
              </button>
            </form>
          </div>
          <div id="box2" class="w-50">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Name</th>
                  <th scope="col">Email</th>
                  <th scope="col">Age</th>
                  <th scope="col">Update</th>
                  <th scope="col">Delete</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="user in revUsers">
                  <th scope="row">{{ user.id }}</th>
                  <td>{{ user.name }}</td>
                  <td>{{ user.email }}</td>
                  <td>{{ user.age }}</td>
                  <td>
                    <button class="btn btn-primary" @click="upUser(user.id)">
                      Update
                    </button>
                  </td>
                  <td>
                    <button class="btn btn-danger" @click="delUser(user.id)">
                      Delete
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      email: "",
      age: "",
      users: [{ id: 1, name: "Asilbek", email: "asilbek@gmail.com", age: 16 }],
      errorAlert: "",
      error: false,
      changeUser: null,
    };
  },

  methods: {
    addUser() {
      if (this.changeUser != null) {
        let findUserById = this.users.find(
          (user) => user.id == this.changeUser
        );
        findUserById.name = this.name;
        findUserById.email = this.email;
        findUserById.age = this.age;
        this.changeUser = null;
        (this.name = ""), (this.email = ""), (this.age = "");
      } else if (this.name && this.email && this.age) {
        let newUser = {
          id: this.users.length + 1,
          name: this.name,
          email: this.email,
          age: this.age,
        };
        this.users.push(newUser);
        (this.name = ""),
          (this.email = ""),
          (this.age = ""),
          (this.error = false);
      } else {
        this.error = true;
        this.errorAlert = "Iltimos bo'sh joyni to'ldring";
      }
    },
    delUser(id) {
      this.users = this.users.filter((user) => user.id != id);
    },
    upUser(id) {
      let findUserById = this.users.find((user) => user.id == id);
      this.name = findUserById.name;
      this.email = findUserById.email;
      this.age = findUserById.age;
      this.changeUser = id;
    },
  },
  computed: {
    revUsers() {
      return this.users.reverse();
    },
  },
};
</script>
