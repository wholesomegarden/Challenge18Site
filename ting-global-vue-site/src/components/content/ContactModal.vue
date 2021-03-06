<template>
  <div :class="classes">
    <div class="modal__container">
      <i class="modal__close fa fa-times" @click="closeModal" />
      <h2 class="modal__heading">{{ heading }}</h2>
      <p class="modal__text">{{ text }}</p>
    </div>
    <div class="modal__backdrop" @click="closeModal" />
  </div>
</template>

<script>
export default {
  props: {
    active: Boolean,
    error: Boolean,
  },
  inject: ["closeModal"],
  computed: {
    classes() {
      return {
        modal: true,
        active: this.active,
        error: this.error,
      };
    },
    heading() {
      return !this.error ? "Thank you for reaching out!" : "An error occured";
    },
    text() {
      return !this.error
        ? "We'll be in touch soon."
        : "Please try again in a few moments.";
    },
  },
};
</script>

<style lang="scss">
@import "../../sass/base.scss";
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  visibility: hidden;
  transition: all 0.5s;
  z-index: 9999;

  &.active {
    opacity: 1;
    visibility: visible;
  }

  &__backdrop {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(#fff, 0.7);
  }

  &__container {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%) scale(0);
    width: calc(100% - 2 * #{$padding-sides-mobile});
    max-width: 45rem;
    background-color: #fff;
    padding: 3rem 3rem 4rem;
    text-align: center;
    box-shadow: $boxshadow2;
    border-radius: 1rem;
    transition: all 0.5s;
    z-index: 99999;
  }

  &.active &__container {
    transform: translate(-50%, -50%) scale(1);
  }

  &__close {
    font-size: 2rem;
    color: $color-blue-1;
    margin-bottom: 2.5rem;
    transition: color 0.5s;
    cursor: pointer;

    &:hover {
      color: $color-azure;
    }

    @include respond(mobile) {
      font-size: 1.8rem;
    }
  }

  &.error &__close {
    color: $color-error;

    &:hover {
      color: $color-azure;
    }
  }

  &__heading {
    color: $color-blue-2;
    letter-spacing: initial;
    margin-bottom: 2rem;
    font-weight: 700;
    font-size: 2.5rem;
  }

  &.error &__heading {
    color: $color-error;
  }

  &__text {
    font-size: 1.65rem;

    @include respond(mobile) {
      font-size: 1.5rem;
    }
  }
}
</style>
