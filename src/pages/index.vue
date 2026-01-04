<template>
  <div id="app">
    <app-header 
      :active-section="activeSection" 
      @navigate="scrollToSection"
    />

    <main class="main-content">
      <section1 @section-active="updateActiveSection" />
      
      <section2 />
      
      <section3 />
      

    </main>
  </div>
</template>

<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { ScrollToPlugin } from 'gsap/ScrollToPlugin';
import AppHeader from '../components/header.vue';
import Section1 from '../components/section-1.vue';
import Section2 from '../components/section-2.vue';
import Section3 from '../components/section-3.vue';

gsap.registerPlugin(ScrollTrigger, ScrollToPlugin);

export default {
  name: 'IndexPage',
  components: {
    AppHeader,
    Section1,
    Section2,
    Section3,
  },
  data() {
    return {
      activeSection: 'plan'
    };
  },
  mounted() {
    this.$nextTick(() => {
      this.initSmoothScroll();
      this.initSectionDetection();
    });
  },
  methods: {
    initSmoothScroll() {
    },

    initSectionDetection() {
      const sections = ['plan', 'design', 'build'];
      
      sections.forEach((section, index) => {
        ScrollTrigger.create({
          trigger: '.section-1-wrapper',
          start: `top+=${index * 66.66}% center`,
          end: `top+=${(index + 1) * 66.66}% center`,
          onEnter: () => this.updateActiveSection(section),
          onEnterBack: () => this.updateActiveSection(section),
        });
      });
    },

    updateActiveSection(section) {
      this.activeSection = section;
    },

    scrollToSection(sectionId) {
      let scrollPosition = 0;
      
      if (sectionId === 'plan') {
        scrollPosition = 0;
      } else if (sectionId === 'design') {
        scrollPosition = window.innerHeight * 0.66;
      } else if (sectionId === 'build') {
        scrollPosition = window.innerHeight * 1.33;
      }
      
      gsap.to(window, {
        duration: 1,
        scrollTo: {
          y: scrollPosition,
          autoKill: true
        },
        ease: 'power2.inOut'
      });
    }
  },
  beforeDestroy() {
    ScrollTrigger.getAll().forEach(trigger => trigger.kill());
  }
};
</script>

<style lang="scss">
  *,
  *::before,
  *::after {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  html {
    scroll-behavior: smooth;
    overflow-x: hidden;
  }

  body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, 
                Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    background: #000;
    color: #fff;
    overflow-x: hidden;
    line-height: 1.6;
  }

  #app {
    width: 100%;
    min-height: 100vh;
    overflow-x: hidden;
  }

  .main-content {
    width: 100%;
    padding-top: 0; 
  }

  ::-webkit-scrollbar {
    width: 10px;
  }

  ::-webkit-scrollbar-track {
    background: #1a1a1a;
  }

  ::-webkit-scrollbar-thumb {
    background: #a8ff35;
    border-radius: 5px;
  }

  ::-webkit-scrollbar-thumb:hover {
    background: #95e62a;
  }

  ::selection {
    background: #a8ff35;
    color: #000;
  }

  ::-moz-selection {
    background: #a8ff35;
    color: #000;
  }

  img {
    max-width: 100%;
    height: auto;
    display: block;
  }

  a {
    color: inherit;
    text-decoration: none;
  }

  button {
    font-family: inherit;
    cursor: pointer;
  }

  .container {
    max-width: 1400px;
    margin: 0 auto;
    padding: 0 3rem;
  }

  .text-center {
    text-align: center;
  }

  @media (max-width: 1024px) {
    .container {
      padding: 0 2rem;
    }
  }

  @media (max-width: 768px) {
    .container {
      padding: 0 1.5rem;
    }
  }

  @media (max-width: 480px) {
    .container {
      padding: 0 1rem;
    }
  }
</style>