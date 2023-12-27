<template>
  <v-progress-linear class="loader" color="rgb(24, 103, 192)" indeterminate :height="10"></v-progress-linear>
</template>

<script>
export default {
  name:'loader'

}
</script>

<style scoped>
.loader{
  position: absolute;
}
</style>
