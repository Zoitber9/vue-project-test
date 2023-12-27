<template>
  <v-checkbox :value="value"
              :label="label"
              @change="updateValue">
  </v-checkbox>
</template>

<script>
export default {
  name: 'my-checkbox',
  props: {
    value: {
      type: Boolean,
      required: true
    },
    label: {
      type: String,
      required: true
    }
  },
  methods: {
    updateValue(newValue) {
      this.$emit('input', newValue);
    }
  }
};
</script>

<style scoped>

</style>
