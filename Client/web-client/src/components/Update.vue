<template>
  <div class="edit_user">
    <form @submit.prevent="onSubmit" class="row g-3">
      <div class="row-1">
        <label
          for="staticEmail"
          class="col-sm-2 col-form-label col-form-label-1"
          >Account
        </label>
        <label class="account-title">{{ tk }}</label>
      </div>
      <div class="mb-3 row">
        <label for="inputPassword" class="col-sm-2 col-form-label"
          >Password</label
        >
        <div class="col-sm-10">
          <input
            type="password"
            class="form-control"
            id="inputPassword"
            required
            v-model="password"
          />
        </div>
      </div>
      <div class="col-auto">
        <label class="inputPassword inputPassword-lb">Confirm</label>
      </div>
      <div class="col-auto">
        <label for="inputPassword2" class="visually-hidden">Password</label>
        <input
          type="password"
          class="form-control"
          id="inputPassword2"
          placeholder="Password"
          required
          v-model="newpass"
        />
      </div>
      <div class="col-auto">
        <button type="submit" class="btn btn-primary mb-3">submit</button>
      </div>
    </form>
  </div>
</template>

<script>
// import axios from 'axios'
// import ListUser from './ListUser.vue';
export default {
  methods: {
    onSubmit() {
      if (this.password === this.newpass) {
        console.log(this.tk, this.password, this.newpass);
      } else {
        console.log("that bai");
      }
    },
  },
  props: ["index", "tk", "mk"],
  data() {
    return {
      password: "",
      newpass: "",
    };
  },
};
</script>

<style>
.edit_user {
  width: 60%;
  margin: 0 auto;
  margin-bottom: 10px;
}
.form-label {
  right: 0;
}
.row-1 {
  display: flex;
  margin-bottom: 10px;
}
.inputPassword-lb {
  margin-left: 4px;
  margin-right: 13px;
  padding-top: 5px;
  font-size: 1.08rem;
}
.col-form-label-1 {
  margin-right: 5px;
  margin-bottom: 10px;
  padding-right: 22px;
}
.account-title {
  padding-top: 7px;
  font-size: 1.1rem;
}
</style>
