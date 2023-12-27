<template>
  <v-card class="sidebar">
    <v-form class="form" @submit.prevent>
      <h2>Filters</h2>
      <div class="sidebar__inputs">
        <my-input v-model="minAge" :rules="ageRules" label="Min Age" type="number" required></my-input>
        <my-input v-model="maxAge" :rules="ageRules" label="Max Age" type="number" required></my-input>
      </div>
      <div class="sidebar__checkboxes">
        <my-checkbox value="value" label="Male" v-model="gender.male"/>
        <my-checkbox value="value" label="Female" v-model="gender.female"/>
      </div>
      <div class="sidebar__btns">
        <my-button color="primary" :disabled="!isAnyFilterApplied" @click="applyFilters">Apply</my-button>
        <my-button color="primary" :disabled="!isAnyFilterApplied" @click="resetFilters">Reset</my-button>
      </div>
    </v-form>
  </v-card>
</template>

<script>
import MyInput from "@/components/UI/MyInput.vue";
import MyCheckbox from "@/components/UI/MyCheckbox.vue";
import MyButton from "@/components/UI/MyButton.vue";

export default {
  name: 'sidebar',
  components: {MyButton, MyCheckbox, MyInput},
  props: {
    filters: {
      type: Object,
      default: () => ({
        maxAge: '',
        minAge: '',
        gender: {
          male: false,
          female: false
        }
      })
    }
  },
  data() {
    return {
      maxAge: '',
      minAge: '',
      gender: {
        male: false,
        female: false
      },
      ageRules: [
        v => !!v || 'Enter age',
        v => (v >= 0 && v <= 100) || 'Enter age from 0 to 100',
        v => !this.maxAge || !this.minAge || v >= this.minAge || 'The Max Age must' +
          ' be greater than or equal to the Min Age'
      ]
    };
  },
  computed: {
    isAnyFilterApplied() {
      return (
        this.maxAge !== '' ||
        this.minAge !== '' ||
        this.gender.male ||
        this.gender.female
      );
    }
  },
  methods: {
    applyFilters() {
      const filters = {
        maxAge: this.maxAge,
        minAge: this.minAge,
        gender: this.gender
      };
      this.$emit('apply-filters', filters);
    },
    resetFilters() {
      this.maxAge = '';
      this.minAge = '';
      this.gender.male = false;
      this.gender.female = false;
      this.$emit('reset-filters');
    }
  }
};
</script>

<style scoped>
.sidebar{
    width: 300px;
}

.sidebar__inputs {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.sidebar__btns {
  display: flex;
  flex-direction: column;
  gap: 0.625rem;
}

.sidebar__checkboxes {
  margin-top: 0.625rem;
  display: flex;
}

h2 {
  text-align: center;
  padding-bottom: 1rem;
}

</style>
