<template>
  <div class="UserCardGallery">
    <div v-for="user in users" :key="user.id">
      <div class="card">
        <img :src="user.avatar" alt="">
        <p class="nameOfUser">{{ user.first_name }} {{ user.last_name }}</p>
        <p class="clickableParagraf" @click="toggleEmail(user)">Contact</p>
      </div>
    </div>
  </div>
  <div class="pagination">
      <button @click="fetchData(1)" :disabled="page === 1">1</button>
      <button @click="fetchData(page + 1)" :disabled="page === 2">2</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [],
      page: 1,
      totalPages: 0,
    };
  },
  mounted() {
    this.fetchData(this.page);
  },
  methods: {
    fetchData(page) {
      fetch(`https://reqres.in/api/users?page=${page}`, {
        method: "GET",
      })
        .then((response) => {
          response.json().then((data) => {
            this.users = data.data;
            this.page = page; 
          });
        })
        .catch((err) => {
          console.error(err);
        });
    },
    toggleEmail(user) {
      const emailLink = `mailto:${user.email}`;
      window.location.href = emailLink;
    },
  },
};
</script>

<style scoped>
</style>
