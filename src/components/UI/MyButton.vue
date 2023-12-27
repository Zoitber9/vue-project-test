<template>
  <v-btn v-bind="$props" @click="handleClick">
    <slot></slot>
  </v-btn>
</template>

<script>
export default {
  name:'my-button',
  methods: {
    handleClick(event) {
      this.$emit('click', event);
    }
  }
};
</script>
