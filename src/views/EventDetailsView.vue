<template>
  <div class="event-info">
    <div class="event-info__content">
      <h1 class="event-info__title">Who Are We?</h1>
      <p class="event-info__description">
        We're a full-cycle event agency creating bold, memorable experiences with a team of creatives and planners.
      </p>
      <h1 class="event-info__title">Where We Are?</h1>
      <p class="event-info__description">
        Headquartered in the city, we run events worldwide—wherever our clients need us.
      </p>
      <h1 class="event-info__title">What We Do?</h1>
      <p class="event-info__description">
        We handle everything from concept to execution for corporate, brand, and private events.
      </p>
      <router-link to="/" class="event-info__back-link">Back to Home</router-link>
    </div>
  </div>
</template>

<style scoped lang="scss">
.event-info {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  padding: 0.5rem;
  overflow: hidden;

  &__content {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  &__title {
    font-size: 18px;
    margin-bottom: 1rem;
  }

  &__description {
    max-width: 600px;
    margin: 0 auto 2rem;
    line-height: 1.6;
    font-size: 14px;
  }

  &__back-link {
    display: inline-block;
    padding: 10px 20px;
    background-color: $color-yellow;
    color: white;
    text-decoration: none;
    border-radius: 4px;
    transition: all $animation-speed ease;

    &:hover {
      transform: translateY(-3px);
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
  }

  @media (min-width: $mobile) {
    padding: 1rem;

    &__description {
      font-size: 16px
    }
  }

  @media (min-width: $tablet) {
    padding: 2rem
  }
}
</style>

