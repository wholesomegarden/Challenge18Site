<template>
  <p class="error-message">
    {{ message }}
  </p>
</template>

<script>
export default {
  props: {
    error: [Error, String, Object]
  },
  computed: {
    message() {
      if (typeof this.error === "string") {
        return this.error;
      } else {
        return (
          this.error.response?.data?.msg ||
          "An error occured. Please try again in a few moments."
        );
      }
    }
  }
};
</script>

<style lang="scss">
@import "@/assets/sass/base.scss";

.error-message {
  color: $color-error;
  font-weight: 500;
  font-size: 1.65rem;
  text-align: center;
  padding: 0 $padding-sides-mobile;

  @include respond(mobile) {
    font-size: 1.5rem;
  }
}

.form .error-message,
.checkout .error-message,
.modal .error-message,
.button + .error-message,
.challenge-options__wrapper + .error-message {
  margin-top: 4rem;

  @include respond(mobile) {
    margin-top: 3rem;
  }
}
</style>
