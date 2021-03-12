<template>
  <div class="container">
    <h1>Scroll to see animation</h1>
    <div class="btns">
      <!-- <button @click="playAnimation">play</button> -->
      <button @click="setSpeed" id="increase">slow down</button>
      <button @click="setSpeed" id="decrease">speed up</button>
      <span class="speed">{{ speed.toFixed(1) }}</span>
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
    props: ['speed'],
    data() {
      return {
        tlForward: null,
        duration: 0.03,
        laptops: ['laptop0', 'laptop1', 'laptop2', 'laptop3', 'laptop4', 'laptop5', 'laptop6']
      }
    },
    mounted() {
      console.log('mounted');
      this.tlForward = null
      this.tlForward = gsap.timeline({
        paused: true,
        scrollTrigger: {
          trigger: '.container',
          pin: true,
          scrub: this.speed
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
              duration: this.duration,
              display: 'block'
            }, '-=0.001')
          }

          if(index !== arr.length - 1) {
            tl.to(item, {
              duration: this.duration,
              display: 'none'
            })
          }
        })
      },
      playAnimation() {
        this.tlForward.seek(0);
        this.tlForward.play();
      },
      setSpeed(event) {
        console.log(event);
        let value = 0;
        event.target.id === 'increase' ? value = 0.1 : value = -0.1;
        this.$emit('setSpeed', value);
      }
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

    background: coral;
  }
  .laptop-container {
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
  .speed {
    color: white;
    margin-left: 10px;
  }
</style>