<template>
  <div>
    <Nuxt />
    <SpinningLogoBg />
  </div>
</template>

<script>
import SpinningLogoBg from "../components/extras/SpinningLogoBg";
import socket from "socket.io-client";
import { baseURL } from "../assets/util/axios";

export default {
  components: { SpinningLogoBg },
  data() {
    return {
      io: socket(baseURL)
    };
  },
  computed: {
    isLoggedIn() {
      return this.$store.getters.isAuth;
    },
    user() {
      return this.$store.getters.user;
    }
  },
  methods: {
    initSocket() {
      this.io.on("allBoards", ({ challenges }) =>
        this.$store.dispatch("results/updateResults", challenges)
      );
      if (this.user) {
        this.io.emit("joinRoom", this.user.id);
      }
    }
  },
  watch: {
    isLoggedIn(value) {
      if (value) {
        this.$router.replace("/dashboard");
        this.io.emit("joinRoom", this.user.id);
      } else if (this.$route.meta.requiresAuth) {
        this.$router.replace("/");
      }
    }
  },
  mounted() {
    this.initSocket();
  },
  provide() {
    return {
      io: this.io
    };
  }
};
</script>
