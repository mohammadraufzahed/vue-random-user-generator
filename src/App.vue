<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
export default {
  methods: {
    async getUser() {
      this.loading = true;
      const user = await fetch("https://randomuser.me/api", {
        method: "GET",
      })
        .then((data) => data.json())
        .then((json) => json.results[0]);
      this.loading = false;
      return {
        name: {
          first: user.name.first,
          last: user.name.last,
        },
        profile: user.picture.large,
        email: user.email,
      };
    },
    async updateUser() {
      this.person = await this.getUser();
    },
  },
  async beforeMount() {
    console.clear();
    this.person = await this.getUser();
  },
  data() {
    return {
      person: {
        name: {
          first: "Mohammad",
          last: "Raufzahed"
        },
        profile: "https://randomuser.me/api/portraits/men/54.jpg",
        email: "mohammadraufzahed@protonmail.com"
      },
      loading: false,
    };
  },
};
</script>

<template>
  <div class="container">
    <img class="profile_image" :src="person.profile" />
    <h1 class="title">{{ person.name.first }} {{ person.name.last }}</h1>
    <button class="button" @click="updateUser">Update the user</button>
  </div>
  <div class="loader" v-if="loading == true">
    <img src="/loader.gif" width="100" height="100" />
  </div>
</template>

<style>
.container {
  overflow-x: hidden;
  font-family: "Roboto";
  display: flex;
  flex-direction: column;
  width: max-content;
  height: max-content;
  margin: 0 auto;
  justify-content: center;
  align-items: center;
  width: 100vw;
  min-height: 100vh;
}
.profile_image {
  border-radius: 50%;
  border: 4px solid blue;
  transition: 400ms ease;
  transition-property: scale;
}
.profile_image:hover {
  scale: 1.1;
}
.title {
  font-weight: bolder;
}

.button {
  width: max-content;
  border: 0;
  background-color: blue;
  color: white;
  font-weight: bold;
  padding: 1vw;
  cursor: pointer;
  transition: 200ms ease;
  transition-property: filter;
}
.button:hover {
  filter: drop-shadow(1px 10px 4px #4444dd);
}
.loader {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.7);
}
</style>
