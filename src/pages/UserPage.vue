<template>
  <loader v-if="isUsersLoading"/>
  <div class="container">
    <div class="sidebar">
      <sidebar
        :filters="filters"
        @apply-filters="applyFilters"
        @reset-filters="resetFilters"
      />
    </div>
    <div class="main">
      <my-input class="search-input"
                prepend-inner-icon="mdi-magnify"
                placeholder="Search"
                v-model="searchQuery">

      </my-input>
      <user-list :users="filteredUsers"/>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import UserList from "@/components/userList.vue";
import Sidebar from "@/components/sidebar.vue";
import MyInput from "@/components/UI/MyInput.vue";
import Loader from "@/components/UI/Loader.vue";

export default {
  components: {Loader, MyInput, Sidebar, UserList},
  data() {
    return {
      users: [],
      isUsersLoading: false,
      searchQuery: "",
      filters: {
        maxAge: "",
        minAge: "",
        gender: {
          male: false,
          female: false,
        },
      },
    };
  },
  methods: {
    applyFilters(filterValues) {
      this.filters = filterValues;
    },
    resetFilters() {
      this.filters = {
        maxAge: "",
        minAge: "",
        gender: {
          male: false,
          female: false,
        },
      };
    },
    async fetchUsers() {
      try {
        this.isUsersLoading = true;
        const res = await axios.get("https://randomuser.me/api/?results=32");
        this.users = res.data.results;
      } catch (e) {
        alert("Error");
      } finally {
        this.isUsersLoading = false;
      }
    },
  },
  computed: {
    filteredUsers() {
      const {maxAge, minAge, gender} = this.filters;
      return this.users.filter((user) => {
        const isAgeMatch =
          (maxAge === "" || user.dob.age <= maxAge) &&
          (minAge === "" || user.dob.age >= minAge);
        const isGenderMatch =
          (!gender.male || user.gender === "male") &&
          (!gender.female || user.gender === "female") ||
          (gender.male && gender.female);
        const isSearchMatch =
          this.searchQuery.trim() === "" ||
          user.name.first
            .toLowerCase()
            .includes(this.searchQuery.toLowerCase());
        return isAgeMatch && isGenderMatch && isSearchMatch;
      });
    },
  },
  mounted() {
    this.fetchUsers();
  },
};
</script>

<style scoped>


.container {
  display: flex;
  padding: 0 4%;
}

.sidebar {
  background-color: #f0f0f0;
  padding: 20px;
}

.main {
  width: 75%;
  padding: 20px;
}

.search-input {
  width: 100%;
  text-align: center;
}

@media (max-width: 675px) {
  .container {
    flex-direction: column;
  }

    .sidebar{
        width: 100%;
    }

  .main {
    margin: auto;
  }
}
</style>
