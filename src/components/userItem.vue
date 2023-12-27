<template>
  <div class="card">
    <img :src="user.picture.large" alt="Аватар пользователя" class="avatar">
    <h2 class="name">{{ user.name.first }} {{ user.name.last }}</h2>
    <p class="gender">{{ user.gender }}</p>
    <p class="age">{{ user.dob.age }} years</p>
    <p>
      <a :href="'mailto:' + user.email" class="email-link">{{ user.email }}</a>
    </p>
    <p>
      <a :href="'tel:' + user.phone" class="phone-link">{{ user.phone }}</a>
    </p>
  </div>
</template>

<script>
export default {
  props: {
    user: {
      type: Object,
      required: true
    }
  }
}
</script>

<style>
.card {
  width: 270px;
  height: 320px;
  border-radius: .5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #fff;
}

.email-link {
  font-size: 0.5rem;
}

.gender {
  font-size: 0.9rem;
  color: #888;
  margin-bottom: 0.5rem;
}

.age {
  font-size: 0.75rem;
  color: #888;
}

.email-link, .phone-link {
  font-size: 0.9rem;
  color: #333;
  text-decoration: none;
}

.avatar {
  border-radius: 50%;
}
</style>
