<template>
  <article class="team-member">
    <a
      v-if="member.link"
      :href="member.link"
      rel="noopener noreferrer"
      target="_blank"
    >
      <TeamMemberImg />
    </a>
    <TeamMemberImg v-else />
    <div class="team-member__card">
      <h3 class="team-member__name">
        {{ member.name }}
      </h3>
      <span v-if="member.role" class="team-member__role">
        {{ member.role }}
      </span>
      <p class="team-member__description">
        {{ member.description }}
      </p>
    </div>
  </article>
</template>

<script>
import TeamMemberImg from "./TeamMemberImg";

export default {
  components: { TeamMemberImg },
  props: {
    member: Object
  },
  provide() {
    return {
      member: this.member
    };
  }
};
</script>

<style lang="scss">
@import "@/assets/sass/base.scss";

.team-member {
  display: flex;
  flex-direction: column;
  align-items: center;

  &__img {
    display: block;
    border: 0.6rem solid #eee;
    border-radius: 6rem;
    height: 16rem;
    width: 14rem;
    background-size: cover;
    background-position: center;
    margin-bottom: -8rem;
    position: relative;
    z-index: 10;
  }

  &__card {
    flex: 1;
    padding: 11rem 1.75rem 3rem;
    box-shadow: $boxshadow2;
    border-radius: 0.8rem;
    text-align: center;
    position: relative;
    overflow: hidden;

    @include respond(mobile) {
      padding-top: 10rem;
    }

    &::before {
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 0.6rem;
      background-color: $color-blue-2;
    }
  }

  &__name {
    font-weight: 500;
    font-size: 2.3rem;
  }

  &__role {
    display: block;
    font-size: 1.7rem;
    color: #888;
    margin-top: 0.8rem;
  }

  &__description {
    font-size: 1.55rem;
    line-height: 1.65;
    margin-top: 2rem;
  }
}
</style>
