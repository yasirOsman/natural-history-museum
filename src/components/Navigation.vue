<template>
  <div class="navbar">
    <RouterLink :to="{ name: 'space' }">
      <font-awesome-icon :icon="['fas', 'building-columns']" style="color: white" size="3x" />
    </RouterLink>
    <span class="navbar__title">Natural History Museum</span>
    <font-awesome-icon
      class="navbar__menu-icon"
      :icon="['fas', 'bars']"
      style="color: white"
      size="3x"
    />
  </div>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

export default {
  name: 'Navigation',
  components: { FontAwesomeIcon }
}
</script>

<style lang="scss" scoped>
.navbar {
  background-color: rgba(0, 0, 0, 0.5);
  padding: 1rem;
  position: fixed;
  width: 100%;
  top: 0;
  z-index: 99999;

  &__title {
    font-size: 2rem;
    font-weight: bold;
    color: white;
    margin-left: 2rem;
    font-family: Arial, serif;
  }

  &__menu-icon {
    position: absolute;
    top: 50%;
    right: 4rem;
    transform: translateY(-50%);
    color: white;
  }
}
</style>
