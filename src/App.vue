<template>
  <div class="app">
    <user-page/>
  </div>
</template>

<script>
import UserPage from "@/pages/UserPage.vue";

export default {
  components: {UserPage}
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat&display=swap");

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}
</style>
