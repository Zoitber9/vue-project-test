<template>
  <div class="user-block">
    <h2> User List </h2>
    <div class="user-list">
      <UserItem
        v-for="user in users"
        :key="user.id"
        :user="user"
      />
    </div>
    <h2 v-if="users.length === 0">
      User list is empty
    </h2>
  </div>
</template>

<script>
import UserItem from "@/components/UserItem.vue";

export default {
  props: {
    users: {
      type: Array,
      required: true
    }
  },
  components: {
    UserItem
  },
};
</script>

<style scoped>
.user-block {
  text-align: center;
}

h1 {
  padding-bottom: 0.625rem;
}

.user-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 1rem;
}

h2 {
  margin: 0 0 1rem 0;
}

@media (max-width: 1280px) {
  .user-list {
    justify-content: space-around;
  }
}
</style>
