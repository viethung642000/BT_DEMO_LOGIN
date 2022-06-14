<template>
  <!-- @close="handleClick" -->
  <div class="list">
    <User
      v-for="user in users"
      v-bind:key="user.index"
      v-bind:userid="user"
      @detele="deteleUser"
    />
    <Add v-if="showAdd" :usersList="users" @adduser="addUser" />
    <span @click="handleClickAdd"><a class="list_user_boxname">Thêm</a></span>
  </div>
</template>

<script>
import User from "./User.vue";
import Add from "./Add.vue";
import { ref } from "vue";
import axios from "axios";

export default {
  name: "ListUser",
  props: {},
  data() {
    return {
      showAdd: false,
    };
  },
  setup() {
    const users = ref([
      // {
      //   index: 1,
      //   tk: "kien123",
      //   ten: "Võ Trung Kiên",
      //   mk: "123",
      // },
      // {
      //   index: 2,
      //   tk: "hung123",
      //   ten: "Hồ Việc Hưng",
      //   mk: "123",
      // },
      // {
      //   index: 3,
      //   tk: "chien123",
      //   ten: "Thiện Chiến",
      //   mk: "123",
      // },
    ]);
    const addUser = async (newUser) => {
      try {
        for(let i; i<this.users.length; i++){
          if(newUser.tk !== this.users[i].tk){
            const res = await axios.post("", newUser);
            users.value.push(res.data);
          }
        }
      } catch (error) {
        alert("tài khoản đã tồn tại");
      }
    };
    const deteleUser = async (index) => {
      try {
        for(let i; i<this.users.length; i++){
          if(index !== this.users[i].index){
            await axios.delete(``);
            users.value = users.value.filter((user) => user.index !== index);
          }
        }
      } catch (error) {
        alert("khong the xoa tai khoan dang dang nhap");
      }
    };
    const getAll = async () => {
      try {
        const res = await axios.get(
          "https://jsonplaceholder.typicode.com/todos?_limit=5"
        );
        console.log(res.data);
        users.value = res.data;
      } catch (ex) {
        console.log("error");
      }
    };
    getAll();
    return {
      users,
      addUser,
      deteleUser,
    };
  },
  components: {
    User,
    Add,
  },
  methods: {
    handleClickAdd() {
      this.showAdd = !this.showAdd;
      console.log(this.users.index);
    },
  },
};
</script>

<style>
.list {
  width: 60%;
  height: 100%;
  margin: 0 auto;
  margin-top: 100px;
  border: 1px solid rgba(0, 0, 0, 0.09);
  border-radius: 10px;
  padding-top: 20px;
  padding-bottom: 10px;
}
.list_user_boxname {
  margin-left: 5px;
  cursor: pointer;
  color: rgba(0, 0, 0, 0.5);
}
</style>
