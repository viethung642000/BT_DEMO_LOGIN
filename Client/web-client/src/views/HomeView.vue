<template>
  <div class="user">
    <ListUser />
  </div>
</template>

<script>
// @ is an alias to /src
import ListUser from "../components/ListUser.vue";

export default {
  name: "HomeView",
  components: {
    ListUser,
  },
};
</script>
