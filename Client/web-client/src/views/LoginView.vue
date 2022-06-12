<template>
  <div style="width: 300px; margin: auto">
    <h1>Login</h1>
    <form @submit.prevent="CheckUser">
      <label class="form-label" for="user">Username</label>
      <div class="form-outline mb-4">
        <input
          type="text"
          id="user"
          class="form-control"
          v-model="user"
          required
        />
      </div>

      <div class="form-outline mb-4">
        <label class="form-label" for="password">Password</label>
        <input
          type="password"
          id="password"
          class="form-control"
          v-model="pass"
          required
        />
      </div>

      <button type="submit" class="btn btn-primary btn-block">Sign in</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
import { ref } from "vue";

export default {
  name: "IndexView",
  methods: {
    CheckUser: function () {
      const userdata = ref([]);
      const AuthUser = async () => {
        try {
          const res = await axios.get(
            "https://localhost:7222/api/Albums/" + this.user
          );

          userdata.value = res.data;
          // console.log(this.user);
          if (userdata.value != null) {
            await this.CheckPass(userdata);
          } else {
            console.log("User dont exist");
          }
        } catch (error) {
          alert("User is incorrect...");
        }
      };
      AuthUser();
    },
    CheckPass: function (userdata) {
      if (this.pass.trim() === userdata.value.title.trim()) {
        this.$router.push("/next");
      } else {
        alert("Login fail...");
      }
    }
  }
};
</script>

<!-- setup() {
    const data = ref({
      user: "",
      pass: ""
    });

    const submit = async () => {
      try {
        const respone = await axios.post("/api/Auth/login", this.data, {
          withCredentials: true
        });
        console.log(respone.data);
      } catch (error) {
        console.log(error);
      }
    };

    return {
      data,
      submit
    };
  } -->
