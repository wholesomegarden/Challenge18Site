<template>
  <form class="form" @submit.prevent="submitHandler">
    <div class="form__field">
      <label for="name" class="form__label">Name</label>
      <input
        v-model="formData.name"
        id="name"
        name="name"
        placeholder="Your name"
        required
        class="form__input"
      />
    </div>
    <div class="form__field">
      <label for="email" class="form__label">
        Email
      </label>
      <input
        v-model="formData.email"
        id="email"
        name="email"
        placeholder="Your email address"
        type="email"
        required
        class="form__input"
      />
    </div>
    <div class="form__field">
      <label for="phone" class="form__label">Phone</label>
      <input
        v-model="formData.phone"
        id="phone"
        name="phone"
        type="tel"
        required
        placeholder="Your phone number "
        class="form__input"
      />
    </div>
    <div class="form__field">
      <label for="organization" class="form__label"
        >Organization (optional)</label
      >
      <input
        v-model="formData.organization"
        id="organization"
        name="organization"
        placeholder="Your organization"
        class="form__input"
      />
    </div>
    <div class="form__field">
      <label for="role" class="form__label">Role (optional)</label>
      <input
        v-model="formData.role"
        id="role"
        name="role"
        placeholder="Your role in the organization"
        class="form__input"
      />
    </div>
    <div class="form__field">
      <label for="subject" class="form__label">Subject</label>
      <input
        v-model="formData.subject"
        id="subject"
        name="subject"
        required
        placeholder="Subject of your message"
        class="form__input"
      />
    </div>
    <div class="form__field">
      <label for="message" class="form__label">Message</label>
      <textarea
        v-model="formData.message"
        id="message"
        name="message"
        required
        placeholder="Leave your message here"
        class="form__input form__textarea"
      />
    </div>
    <BaseButton variant="blue">Submit</BaseButton>
  </form>
</template>

<script>
export default {
  inject: ["sendMessage"],
  data() {
    return {
      formData: {
        name: "",
        email: "",
        phone: "",
        organization: "",
        role: "",
        subject: "",
        message: "",
      },
    };
  },
  methods: {
    async submitHandler(event) {
      const success = await this.sendMessage(event.target);
      if (success) {
        this.resetForm();
      }
    },
    resetForm() {
      for (let key in this.formData) {
        this.formData[key] = "";
      }
    },
  },
};
</script>

<style lang="scss">
@import "../../sass/base.scss";

.form {
  display: flex;
  flex-direction: column;
  max-width: 70rem;
  margin: auto;
  text-align: initial;

  &__field {
    display: flex;
    flex-direction: column;
    margin-bottom: 2.5rem;

    @include respond(mobile) {
      margin-bottom: 2rem;
    }
  }

  &__label {
    font-weight: 500;
    font-size: 1.6rem;
    margin-bottom: 1rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: relative;

    @include respond(mobile) {
      font-size: 1.5rem;
      margin-bottom: 0.8rem;
    }

    i {
      display: block;
      font-size: 1.8rem;

      @include respond(mobile) {
        font-size: 1.7rem;
      }
    }
  }

  &__input {
    font: inherit;
    font-size: 1.65rem;
    line-height: 1.6;
    padding: 1.2rem 1rem;
    border: 0.2rem solid transparent;
    outline: none;
    border-radius: 0.8rem;
    transition: all 0.4s;
    width: 100%;
    background-color: #fff !important;
    box-shadow: $boxshadow2;

    @include respond(mobile) {
      font-size: 1.5rem;
    }

    &:focus {
      border-color: $color-azure;
    }
  }

  &__textarea {
    resize: none;
    height: 15rem;
  }

  .button {
    margin-top: 1rem;
    font-weight: 600;
    width: 100%;
    padding: 1.25rem;

    @include respond(mobile) {
      padding: 1.1rem;
    }
  }
}
</style>
