<template>
  <section id="section2" class="section2" ref="section2">
    <div class="section2__container">
      <div class="section2__card" ref="card">
        
        <!--plan-->
        <div class="section2__content-slide" ref="slide1">
          <div class="section2__image-wrapper">
            <img :src="imagePlan"
              alt="Plan"
              class="section2__image"
            >
          </div>
          <div class="section2__overlay">
            <h2 class="section2__text">plan</h2>
          </div>
        </div>

        <!--design-->
        <div class="section2__content-slide" ref="slide2">
          <div class="section2__image-wrapper">
            <img :src="imageDesign"               
              alt="Design"
              class="section2__image"
            >
          </div>
          <div class="section2__overlay">
            <h2 class="section2__text">design</h2>
          </div>
        </div>

        <!--build-->
        <div class="section2__content-slide" ref="slide3">
          <div class="section2__image-wrapper">
            <img :src="imageBuild"              
              alt="Build"
              class="section2__image"
            >
          </div>
          <div class="section2__overlay">
            <h2 class="section2__text">build</h2>
          </div>
        </div>

      </div>
    </div>

    <div class="section2__progress" ref="progressBar">
      <div class="section2__progress-fill" ref="progressFill"></div>
    </div>
  </section>
</template>

<script>
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import imagePlan from '@/assets/images/imagePlan.jpg';
import imageDesign from '@/assets/images/imageDesign.jpg';
import imageBuild from '@/assets/images/imageBuild.jpg';

gsap.registerPlugin(ScrollTrigger)

export default {
  name: 'Section2Component',
  data() {
    return {
      imagePlan,
      imageDesign,
      imageBuild,
      scrollTriggerInstance: null,
      contentItems: []
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.initScrollAnimation()
    })
  },
  beforeDestroy() {
    if (this.scrollTriggerInstance) {
      this.scrollTriggerInstance.kill()
    }
  },
  methods: {
    initScrollAnimation() {
      const section = this.$refs.section2
      const slide1 = this.$refs.slide1
      const slide2 = this.$refs.slide2
      const slide3 = this.$refs.slide3
      const progressFill = this.$refs.progressFill

      const slide1Text = slide1.querySelector('.section2__text')
      const slide1Image = slide1.querySelector('.section2__image-wrapper')
      const slide2Text = slide2.querySelector('.section2__text')
      const slide2Image = slide2.querySelector('.section2__image-wrapper')
      const slide3Text = slide3.querySelector('.section2__text')
      const slide3Image = slide3.querySelector('.section2__image-wrapper')

      gsap.set(slide1, { opacity: 1, zIndex: 1 })
      gsap.set([slide2, slide3], { opacity: 0, zIndex: 1 })
      
      gsap.set([slide1Image, slide2Image, slide3Image], { 
        opacity: 0, 
        scale: 0.3,
        transformOrigin: 'center center'
      })
      
      gsap.set([slide1Text, slide2Text, slide3Text], { 
        opacity: 0,
        y: 20
      })

      this.scrollTriggerInstance = ScrollTrigger.create({
        trigger: section,
        start: 'top top',
        end: `+=${window.innerHeight * 4}`,
        pin: true,
        scrub: 1,
        onUpdate: (self) => {
          const progress = self.progress

          gsap.to(progressFill, {
            scaleX: progress,
            duration: 0.1
          })

          //slide 1 plan
          if (progress >= 0 && progress <= 0.33) {
            gsap.set(slide1, { zIndex: 1 })
            
            //background doang
            if (progress <= 0.05) {
              gsap.set(slide1, { opacity: 1 })
              gsap.set(slide1Text, { opacity: 0, y: 20 })
              gsap.set(slide1Image, { opacity: 0, scale: 0.3 })
            }
            //text gambar
            else if (progress > 0.05 && progress <= 0.20) {
              const animProgress = (progress - 0.05) / 0.15
              const textProgress = Math.min(animProgress * 1.8, 1)
              gsap.to(slide1Text, {
                opacity: textProgress,
                y: 20 * (1 - textProgress),
                duration: 0.05
              })
              gsap.to(slide1Image, {
                opacity: animProgress,
                scale: 0.3 + (animProgress * 0.7), // 0.3 -> 1.0
                duration: 0.1
              })
            }
            else if (progress > 0.20) {
              gsap.set(slide1Text, { opacity: 1, y: 0 })
              gsap.set(slide1Image, { opacity: 1, scale: 1 })
            }
          }

          //slide 2 design
          if (progress >= 0.33 && progress <= 0.66) {
            gsap.set(slide2, { opacity: 1, zIndex: 2 }) 
            
            if (progress >= 0.33 && progress <= 0.48) {
              const animProgress = (progress - 0.33) / 0.15
              const textProgress = Math.min(animProgress * 1.8, 1)
              gsap.to(slide2Text, {
                opacity: textProgress,
                y: 20 * (1 - textProgress),
                duration: 0.05
              })
              gsap.to(slide2Image, {
                opacity: animProgress,
                scale: 0.3 + (animProgress * 0.7), // 0.3 -> 1.0
                duration: 0.1
              })
            }
            else if (progress > 0.48) {
              gsap.set(slide2Text, { opacity: 1, y: 0 })
              gsap.set(slide2Image, { opacity: 1, scale: 1 })
            }
          } else if (progress < 0.33) {
            gsap.set(slide2, { opacity: 0, zIndex: 2 })
            gsap.set(slide2Text, { opacity: 0, y: 20 })
            gsap.set(slide2Image, { opacity: 0, scale: 0.3 })
          }

          //slide 3 build
          if (progress >= 0.66) {
            gsap.set(slide3, { opacity: 1, zIndex: 3 }) 
            
            if (progress >= 0.66 && progress <= 0.81) {
              const animProgress = (progress - 0.66) / 0.15
              const textProgress = Math.min(animProgress * 1.8, 1)
              gsap.to(slide3Text, {
                opacity: textProgress,
                y: 20 * (1 - textProgress),
                duration: 0.05
              })
              gsap.to(slide3Image, {
                opacity: animProgress,
                scale: 0.3 + (animProgress * 0.7), // 0.3 -> 1.0
                duration: 0.1
              })
            }
            else {
              gsap.set(slide3Text, { opacity: 1, y: 0 })
              gsap.set(slide3Image, { opacity: 1, scale: 1 })
            }
          } else {
            gsap.set(slide3, { opacity: 0, zIndex: 3 })
            gsap.set(slide3Text, { opacity: 0, y: 20 })
            gsap.set(slide3Image, { opacity: 0, scale: 0.3 })
          }
        }
      })

      gsap.set(section, { opacity: 1 })
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../assets/styles/main.scss';

  .section2 {
    height: 100vh;
    position: relative;
    overflow: hidden;
    background-color: #111606;

    &__container {
      width: 100%;
      height: 100%;
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    &__card {
      position: relative;
      width: 100%;
      height: 100%;
      overflow: hidden;
    }

    &__content-slide {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      opacity: 0;
      transform-origin: center center;
    }

    &__image-wrapper {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
    }

    &__image {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
    }

    &__overlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 2;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      gap: 1rem;
      background: linear-gradient(
        to bottom,
        rgba(0, 0, 0, 0.3) 0%,
        rgba(0, 0, 0, 0.6) 100%
      );
    }

    &__content-item {
      opacity: 0;
      transform: translateY(30px);
    }

    &__text {
      font-size: 8rem;
      font-weight: 300;
      color: #a8ff35;
      margin: 0;
      text-transform: lowercase;
      font-style: italic;
      line-height: 1;
      text-align: center;

      @media (max-width: 1024px) {
        font-size: 6rem;
      }

      @media (max-width: 768px) {
        font-size: 4rem;
      }

      @media (max-width: 480px) {
        font-size: 3rem;
      }
    }

    &__progress {
      position: absolute;
      bottom: 3rem;
      left: 50%;
      transform: translateX(-50%);
      width: 200px;
      height: 3px;
      background-color: rgba(255, 255, 255, 0.2);
      border-radius: 2px;
      overflow: hidden;
      z-index: 10;

      @media (max-width: 768px) {
        bottom: 2rem;
        width: 150px;
      }

      @media (max-width: 480px) {
        bottom: 1.5rem;
        width: 120px;
      }
    }

    &__progress-fill {
      width: 100%;
      height: 100%;
      background-color: #a8ff35;
      transform-origin: left center;
      transform: scaleX(0);
      border-radius: 2px;
    }

    &__scroll-hint {
      position: absolute;
      top: 50%;
      right: 2rem;
      transform: translateY(-50%);
      color: rgba(255, 255, 255, 0.5);
      font-size: 0.875rem;
      writing-mode: vertical-rl;
      letter-spacing: 2px;
      z-index: 10;
      animation: fadeInOut 2s infinite;

      @media (max-width: 768px) {
        right: 1.5rem;
        font-size: 0.75rem;
      }

      @media (max-width: 480px) {
        display: none;
      }
    }
  }

  @keyframes fadeInOut {
    0%, 100% {
      opacity: 0.3;
    }
    50% {
      opacity: 1;
    }
  }
</style>