<script setup lang="ts">
import Emitter from '~~/utils/emitter';

const scrollTo = useScrollTo();
const route = useRoute();

const handleScrollTo = (target: string) => {
  if (route.path === '/') {
    scrollTo(target);
    return;
  }

  Emitter.emit('route-change', `/${target}`);
};

const downloadResume = () =>{
  const link = document.createElement('a');
  link.href = "/MyResume.pdf"
  link.download = "AnjishnuGangulyResume.pdf"
  link.click()
}
</script>

<template>
  <header
    class="header"
    data-scroll
    data-scroll-sticky
    data-scroll-target="main"
  >
    <nav class="nav">
      <button class="home-link" @click="handleScrollTo('#hero')">
        Anjishnu Ganguly
      </button>
      <ul class="list">
        <li class="link">
          <button @click="handleScrollTo('#portfolio')">Portfolio</button>
        </li>
        <li class="link">
          <button @click="handleScrollTo('#about')">About</button>
        </li>
        <li class="link">
          <button @click="handleScrollTo('#contact')">Contact</button>
        </li>
        <li>
          <button @click="downloadResume()">Resume</button>
        </li>
      </ul>
    </nav>
  </header>
</template>

<style scoped lang="scss">
@keyframes appear {
  0% {
    opacity: 0;
  }

  50% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

.header {
  @include mixins.mobile-padding;
  @include mixins.section-width;

  position: fixed;
  top: 2rem;
  mix-blend-mode: difference;
  z-index: 999;
  animation: appear 2s variables.$ease-in-out;

  .nav {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;

    .home-link {
      font-weight: 700;
    }

    .list {
      display: flex;
      flex-direction: column;
      align-items: flex-end;
      gap: 0.5rem;
      white-space: nowrap;

      @include screens.laptop {
        flex-direction: row;
        gap: 2rem;
      }
    }
  }
}
</style>
