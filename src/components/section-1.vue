<template>
  <div class="section-1-wrapper" ref="wrapper">
    <div class="section-1-container" ref="container">
      
      <div 
        class="pinned-slide slide-plan"
        :class="{ active: activeIndex === 0 }"
        ref="slide0"
      >
        <div class="slide-content">
          <div class="left-panel">
            <div class="nav-pills">
              <span class="pill active">plan</span>
              <span class="pill">design</span>
              <span class="pill">build</span>
            </div>
            
            <div class="text-content">
              <h1 class="slide-title">The sitemap of the experience</h1>
              <p class="slide-description">
                Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy 
                eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam 
                voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet 
                clita kasd gubergren, no sea
              </p>
            </div>
          </div>

          <div class="right-panel">
            <div class="counter">1 / 3</div>
            <div class="icon-box">
                <img :src="iconPlan" alt="Plan">
            </div>
            <div class="image-box">
                <img :src="imagePlan" alt="Plan">
            </div>
          </div>
        </div>
      </div>

      <!-- Design -->
      <div 
        class="pinned-slide slide-design"
        :class="{ active: activeIndex === 1 }"
        ref="slide1"
      >
        <div class="slide-content">
          <div class="left-panel">
            <div class="nav-pills">
              <span class="pill">plan</span>
              <span class="pill active">design</span>
              <span class="pill">build</span>
            </div>
            
            <div class="text-content">
              <h1 class="slide-title">Time to paint the room walls</h1>
              <p class="slide-description">
                Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy 
                eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam 
                voluptua. At vero eos et accusam et justo duo dolores et ea rebum.
              </p>
            </div>
          </div>

          <div class="right-panel">
            <div class="counter">2 / 3</div>
            <div class="icon-box">
                <img :src="iconDesign" alt="Design">
            </div>
            <div class="image-box">
                <img :src="imageDesign" alt="Design">
            </div>
          </div>
        </div>
      </div>

      <!-- Build -->
      <div 
        class="pinned-slide slide-build"
        :class="{ active: activeIndex === 2 }"
        ref="slide2"
      >
        <div class="slide-content">
          <div class="left-panel">
            <div class="nav-pills">
              <span class="pill">plan</span>
              <span class="pill">design</span>
              <span class="pill active">build</span>
            </div>
            
            <div class="text-content">
              <h1 class="slide-title">Magic happens to build it out</h1>
              <p class="slide-description">
                Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy 
                eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam 
                voluptua. At vero eos et accusam et.
              </p>
            </div>
          </div>

          <div class="right-panel">
            <div class="counter">3 / 3</div>
            <div class="icon-box">
                <img :src="iconBuild" alt="Build">
            </div>
            <div class="image-box">
                <img :src="imageBuild" alt="Build">
            </div>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import iconPlan from '@/assets/images/iconPlan.svg';
import iconDesign from '@/assets/images/iconDesign.svg';
import iconBuild from '@/assets/images/iconBuild.svg';
import imagePlan from '@/assets/images/imagePlan.jpg';
import imageDesign from '@/assets/images/imageDesign.jpg';
import imageBuild from '@/assets/images/imageBuild.jpg';

gsap.registerPlugin(ScrollTrigger);

export default {
  name: 'Section1',
  data() {
    return {
        iconPlan,
        iconDesign,
        iconBuild,
        imagePlan,
        imageDesign,
        imageBuild
    };
  },
  mounted() {
    this.$nextTick(() => {
      requestAnimationFrame(() => {
        this.initScrollAnimation();
      });
    });
  },
  methods: {
    initScrollAnimation() {
      const wrapper = this.$refs.wrapper;
      const container = this.$refs.container;
      
      const slidePlan = this.$refs.slide0;
      const slideDesign = this.$refs.slide1;
      const slideBuild = this.$refs.slide2;

      console.log('Plan slide:', slidePlan.querySelector('.slide-title')?.textContent);
      console.log('Design slide:', slideDesign.querySelector('.slide-title')?.textContent);
      console.log('Build slide:', slideBuild.querySelector('.slide-title')?.textContent);

      gsap.set(slidePlan, { opacity: 1, zIndex: 3, visibility: 'visible' });
      gsap.set(slideDesign, { opacity: 0, zIndex: 1, visibility: 'hidden' });
      gsap.set(slideBuild, { opacity: 0, zIndex: 1, visibility: 'hidden' });

      ScrollTrigger.create({
        trigger: wrapper,
        start: 'top top',
        end: '+=300%',
        pin: container,
        pinSpacing: true,
        scrub: 1,
        onUpdate: (self) => {
          const progress = self.progress;
          
          if (progress < 0.375) {
            this.activeIndex = 0;
          } else if (progress < 0.875) {
            this.activeIndex = 1;
          } else {
            this.activeIndex = 2;
          }
        }
      });

      // Transisi 1: Plan -> Design 
      gsap.to(slidePlan, {
        opacity: 0,
        zIndex: 1,
        visibility: 'hidden',
        scrollTrigger: {
          trigger: wrapper,
          start: 'top+=25% top',
          end: 'top+=50% top',
          scrub: true,
        }
      });

      gsap.to(slideDesign, {
        opacity: 1,
        zIndex: 3,
        visibility: 'visible',
        scrollTrigger: {
          trigger: wrapper,
          start: 'top+=15% top',
          end: 'top+=25% top',
          scrub: true,
        }
      });

      // transisi 2: Design -> Build 
      gsap.to(slideBuild, {
        opacity: 1,
        zIndex: 3,
        visibility: 'visible',
        scrollTrigger: {
          trigger: wrapper,
          start: 'top+=25% top',
          end: 'top+=45% top',
          scrub: true,
        }
      });
    }
  },
  beforeDestroy() {
    ScrollTrigger.getAll().forEach(trigger => trigger.kill());
  }
};
</script>

<style lang="scss" scoped>
  .section-1-wrapper {
    width: 100%;
    height: 400vh;
    position: relative;
  }

  .section-1-container {
    width: 100%;
    height: 100vh;
    position: relative;
    overflow: hidden;
  }

  .pinned-slide {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: #111606;
    opacity: 0;
    visibility: hidden;
    will-change: opacity, transform;
  }

  .slide-plan {
    opacity: 1;
    visibility: visible;
    z-index: 3;
  }

  .slide-content {
    width: 100%;
    height: 100%;
    display: grid;
    grid-template-columns: 1fr 1fr;
  }

  .left-panel {
    padding: 4rem 3rem 4rem 6rem;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;  
    transform: translateY(0);  
  }

  .nav-pills {
    display: flex;
    gap: 1rem;
    margin-bottom: 3rem;
  }

  .pill {
    font-size: 2rem;
    font-weight: 300;
    color: rgba(255, 255, 255, 0.3);
    transition: color 0.3s ease;
    text-transform: lowercase;

    &.active {
      color: #a8ff35;
    }
  }

  .text-content {
    max-width: 600px;
  }

  .slide-title {
    font-family: "RecifeDisplay", sans-serif;
    font-size: 3.5rem;
    font-weight: 700;
    font-style: italic;
    line-height: 1.2;
    margin-bottom: 2rem;
    color: #a8ff35;
  }

  .slide-description {
    font-size: 1rem;
    line-height: 1.7;
    color: #a8ff35;
    font-weight: 300;
  }

  .right-panel {
    position: relative;
  }

  .counter {
    font-family: "RecifeDisplay", sans-serif;
    position: absolute;
    top: 4rem;
    right: 4rem;
    font-size: 2rem;
    font-weight: 300;
    color: #a8ff35;
    font-style: italic;
    z-index: 3;
  }

  .icon-box {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 2;

    img {
      width: 140px;
      height: 140px;
      object-fit: contain;
      filter: brightness(0) saturate(100%) invert(88%) sepia(47%) saturate(1352%) hue-rotate(31deg);
    }
  }

  .image-box {
    width: 100%;
    height: 100%;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      opacity: 0.6;
      border-radius: 60px;
    }
  }


  @media (max-width: 1024px) {
    .left-panel {
      padding: 3rem 2rem 3rem 4rem;
    }

    .pill {
      font-size: 1.5rem;
    }

    .slide-title {
      font-size: 2.5rem;
    }

    .counter {
      font-size: 1.5rem;
      top: 3rem;
      right: 2rem;
    }

    .icon-box img {
      width: 100px;
      height: 100px;
    }
  }

  @media (max-width: 768px) {
    .slide-content {
      grid-template-columns: 1fr;
      grid-template-rows: auto 1fr;
    }

    .left-panel {
      padding: 6rem 2rem 2rem 2rem;
      justify-content: flex-start;
    }

    .nav-pills {
      margin-bottom: 2rem;
    }

    .pill {
      font-size: 1.25rem;
    }

    .slide-title {
      font-size: 2rem;
    }

    .slide-description {
      font-size: 0.9rem;
    }

    .counter {
      top: 5.5rem;
      right: 1.5rem;
      font-size: 1.25rem;
    }

    .icon-box {
      top: 30%;
      right: 10%;
      
      img {
        width: 70px;
        height: 70px;
      }
    }
  }

  @media (max-width: 480px) {
    .left-panel {
      padding: 5rem 1.5rem 1.5rem 1.5rem;
    }

    .pill {
      font-size: 1rem;
    }

    .slide-title {
      font-size: 1.5rem;
      margin-bottom: 1rem;
    }

    .slide-description {
      font-size: 0.85rem;
    }
  }
</style>