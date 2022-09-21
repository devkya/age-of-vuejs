<template>
  <form @submit.prevent="submitForm">
    <div>
      <label for="username">id : </label>
      <input type="text" id="username" v-model="username" />
    </div>
    <div>
      <label for="password">pwd : </label>
      <input type="password" id="password" v-model="password" />
    </div>
    <div>
      <button type="submit">Login</button>
    </div>
  </form>
</template>
<script>
import axios from "axios";
export default {
  components: {},
  data() {
    return {
      username: "",
      password: "",
    };
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {
    submitForm: function () {
      console.log(this.username, this.password);
      var url = "https://jsonplaceholder.typicode.com/users";
      var data = {
        username: this.username,
        password: this.password,
      };
      axios
        .post(url, data)
        .then((res) => {
          console.log(res.data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
