<template>
  <v-text-field v-model="inputValue" class="input" type="text" />
</template>

<script>
export default {
  name: 'MyInput',
  props: {
    modelValue: [String, Number]
  },
  computed: {
    inputValue: {
      get() {
        return this.modelValue;
      },
      set(newValue) {
        this.$emit('update:modelValue', newValue);
      }
    }
  }
}
</script>

<style scoped>
</style>
