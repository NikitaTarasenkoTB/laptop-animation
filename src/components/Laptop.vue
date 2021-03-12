<template>
  <div @mousewheel="whellHandler" class="container">
    <h1>Scroll to see animation</h1>
    <div class="btns">
      <!-- <button @click="playAnimation">play</button> -->
    </div>
    <div class="laptop-container">
      <img 
        v-for="item in laptops" 
        :src=" require('../assets/laptop/' + item + '.png') "
        :key="item"
        class="laptop"
      />
    </div>
  </div>
</template>

<script>
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);

  export default {
    data() {
      return {
        tlForward: null,
        laptops: ['laptop0', 'laptop1', 'laptop2', 'laptop3', 'laptop4', 'laptop5', 'laptop6']
      }
    },
    mounted() {
      this.tlForward = gsap.timeline({
        paused: true,
        scrollTrigger: {
          trigger: '.container',
          pin: true,
          scrub: true,
        }
      });
      const laptopsArr = gsap.utils.toArray('.laptop');

      this.createTl(this.tlForward, laptopsArr);
      this.createTl(this.tlForward, laptopsArr.reverse());
    },
    methods: {
      createTl(tl, laptopsArr) {
        laptopsArr.forEach((item, index, arr) => {
          if(index !== 0) {
            tl.to(item, {
              duration: 0.03,
              display: 'block'
            }, '-=0.0001')
          }

          if(index !== arr.length - 1) {
            tl.to(item, {
              duration: 0.03,
              display: 'none'
            })
          }
        })
      },
      playAnimation() {
        this.tlForward.seek(0);
        this.tlForward.play();
      },
      // whellHandler(event) {
      //   event.preventDefault();
      //   this.tlForward.play();
      //   setTimeout(() => {
      //     this.tlForward.pause();
      //   }, 0.05)
      //   console.log(event);
      // }
    }
  }
</script>

<style lang="scss" scoped>
  h1 {
    margin: 0;
    margin-bottom: 50px;
    color: white;
  }
  .btns {
    display: flex;
  }
  .container {
    display: flex;
    align-items: center;
    flex-direction: column;

    width: 99%;
    min-height: 100vh;

    // position: absolute;
    // top: 0;
    // left: 0;

    background: coral;
  }
  .laptop-container {
    // width: 80%;
    // height: 80%; 
    width: 80vw;
    height: 80vh;
    position: relative;
  }
  .laptop {
    display: none;
    position: absolute;
    bottom: 0;
    left: 0;
    //padding-left: 100px;

    width: 60%;
    // height: 100%;
  }
  .laptop:first-of-type {
    display: block;
  }
  .hide {
    display: none;
  }
</style>