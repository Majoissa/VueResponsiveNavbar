<script setup>
import { ref, nextTick, onMounted, onUnmounted} from 'vue';

const isMenuOpen = ref(false);
const selectedIndex = ref(1); // Default to Home
const slider = ref(null);

const toggleMenu = async (event) => {
  event.stopPropagation();
  isMenuOpen.value = !isMenuOpen.value;
  await nextTick();
  if (isMenuOpen.value) {
    moveSlider(selectedIndex.value);
  }
};

const selectItem = async (index) => {
  selectedIndex.value = index;
  await nextTick();
  moveSlider(index);
}

const moveSlider = (index) => {
  const itemHeight = 50;
  const newPosition = index * itemHeight;
  if (slider.value){
    slider.value.style.transform = `translateY(${newPosition}px)`;
  }
}

onMounted(() => {
  moveSlider(selectedIndex.value);
  window.addEventListener('click', closeMenuOnClickOutside);
});

onUnmounted(() => {
  window.removeEventListener('click', closeMenuOnClickOutside);
});

const closeMenuOnClickOutside = (event) =>{
  if (isMenuOpen.value && !event.target.closest('.navbar')){
    isMenuOpen.value = false;
  }
};
</script>

<template>
  <nav class="navbar">
    <div class="navbar__brand">Brand</div>
    <div class="navbar__toggle" @click="toggleMenu">
      <i v-if="!isMenuOpen" class="fas fa-bars"></i>
      <i v-else class="fas fa-times"></i>
    </div>
    <ul :class="{'navbar__menu': true, 'navbar__menu--open': isMenuOpen}" ref="menu">
      <div class="slider" ref="slider" v-if="isMenuOpen"></div>
      <li class="navbar__item" :class="{'selected' : selectedIndex === 0}" @click="() => selectItem(0)"><a href="#">Home</a></li>
      <li class="navbar__item" :class="{'selected' : selectedIndex === 1}" @click="() => selectItem(1)"><a href="#">About</a></li>
      <li class="navbar__item" :class="{'selected' : selectedIndex === 2}" @click="() => selectItem(2)"><a href="#">Services</a></li>
      <li class="navbar__item" :class="{'selected' : selectedIndex === 3}" @click="() => selectItem(3)"><a href="#">Contact</a></li>
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
    cursor: pointer;
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

  .selected {
    background-color: #e0e0e0;
  }

  .slider {
    display: inline-block;
    position: absolute;
    margin-top: 7px;
    left: 15px;
    width: 3px;
    height: 38px; /* Adjust this height to match your item height */
    background-color: #007bff;
    transition: transform 0.3s ease-in-out;

    @media (max-width: 576px) {
      display: inline-block;
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
