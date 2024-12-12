<template>
  <header>
    <div class="header">
      <h1>{{ title }}</h1>
      <i v-if="isUserLoggedIn" class="fa fa-sign-out-alt" @click="handleLogout()"></i>
    </div>
    <Login v-bind:isUserLoggedIn="isUserLoggedIn" />
    <div class="buttons" v-if="isUserLoggedIn">
      <Button v-bind:text="showAddTask ? 'Close' : 'Add Expense'" v-bind:color="showAddTask ? 'red' : '#2196F3'"
        eventName="Add-Task" @Add-Task="handleToggleAddTask" v-if="isHomePage()" />
    </div>
  </header>
</template>

<script>
import Button from "./Button";
import Login from "./Login.vue";

export default {
  name: "Header",
  props: {
    title: String,
    showAddTask: Boolean,
    isUserLoggedIn: Boolean,
  },
  components: {
    Button,
    Login,
  },
  methods: {
    handleToggleAddTask() {
      this.$emit("toggle-AddTask");
    },
    handleLogout() {
      this.$store.commit("userNotAuthenticated");
    },
    isHomePage() {
      //Handle The logic
      if (this.$route.path === "/") {
        return true;
      }
      return false;
    },
  },
  emits: ["toggle-AddTask"],
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  flex-direction: column;
}

.header {
  display: flex;
  align-items: center;
}

.buttons {
  display: flex;
}

.fa-sign-out-alt {
  position: relative;
  left: 150%;
  font-size: 20px;
  color: rgb(8, 8, 8);
}
</style>
