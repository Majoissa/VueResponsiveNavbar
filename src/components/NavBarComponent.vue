<script setup>
import { ref } from 'vue';

const isMenuOpen = ref(false);
const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};
</script>

<template>
  <nav class="navbar">
    <div class="navbar__brand">Brand</div>
    <div class="navbar__toggle" @click="toggleMenu">
      <i v-if="!isMenuOpen" class="fas fa-bars"></i>
      <i v-else class="fas fa-times"></i>
    </div>
    <ul :class="{'navbar__menu': true, 'navbar__menu--open': isMenuOpen}">
      <li class="navbar__item"><a href="#">Home</a></li>
      <li class="navbar__item"><a href="#">About</a></li>
      <li class="navbar__item"><a href="#">Services</a></li>
      <li class="navbar__item"><a href="#">Contact</a></li>
    </ul>
  </nav>
</template>

<style lang="scss">
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 1rem;
  background-color: #333;
  color: #fff;
  position: relative;

  &__brand {
    font-size: 1.5rem;
  }

  &__toggle {
    display: none;
    font-size: 1.5rem;
    cursor: pointer;
  }

  &__menu {
    display: flex;
    list-style: none;
    margin: 0;
    padding: 0;

    @media (max-width: 576px) {
      max-height: 0;
      overflow: hidden;
      flex-direction: column;
      width: 100%;
      transition: max-height 0.3s ease-in-out;

      &--open {
        max-height: 500px; 
      }
    }
  }

  &__item {
    margin-left: 1rem;

    a {
      color: #fff;
      text-decoration: none;
      &:hover {
        text-decoration: underline;
      }
    }
    @media (max-width: 576px) {
      margin: 0.5rem 0;

      a {
        display: block;
        width: 100%;
        padding: 0.5rem 0;
      }
    }
  }
}

@media (max-width: 576px) {
  .navbar {
    flex-direction: column;
    align-items: flex-start;

    &__toggle {
      display: block;
      position: absolute;
      right: 15px;
    }

  }
}
</style>
