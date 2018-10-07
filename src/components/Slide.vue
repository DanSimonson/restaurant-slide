<template>
  <div class='carousel-view'>
    <transition-group class='carousel' tag="div">
      <div v-for="(slide, index) in slides" class='slide' :key="slide.id" :style="{backgroundImage: 'url(' + slides[index].imgLink + ')'}">
        <!--<img :src='slide.imgLink'>-->
        <h4> {{ slide.title }} </h4>
      </div>
    </transition-group>
    <div class='carousel-controls'>
      <button class='carousel-controls__button' @click="previous">prev</button>
      <button class='carousel-controls__button' @click="next">next</button>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Slide',
    data() {
      return {

        slides: [
          {
            imgLink: require('../assets/tapsilog.jpg'),
            title: 'TAPSILOG',
            id: 1
          },
          {
            imgLink: require('../assets/sizzlingSisig.jpg'),
            title: 'SIZZLING SISIG',
            id: 2
          },
          {
            imgLink: require('../assets/pancitCantonSrc.jpg'),
            title: 'PANCIT CANTON',
            id: 3
          },
          {
            imgLink: require('../assets/karekare.jpg'),
            title: 'KARE KARE',
            id: 4
          },
          {
            imgLink: require('../assets/adobongManok.jpg'),
            title: 'ADOBONG MANOK',
            id: 5
          }
        ]
      }
    },
    methods: {
      next() {
        const first = this.slides.shift()
        this.slides = this.slides.concat(first)
      },
      previous() {
        const last = this.slides.pop()
        this.slides = [last].concat(this.slides)
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h4 {
    color: #fff;
  }

  .carousel {
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;

    width: 24em;
    min-height: 25em;
  }

  .slide {
    flex: 0 0 20em;
    height: 20em;
    margin: 1em;
    display: flex;
    justify-content: center;
    align-items: center;
    border: 0.1em dashed #000;
    border-radius: 50%;
    transition: transform 0.3s ease-in-out;
  }

  .slide:first-of-type {
    opacity: 0;
  }

  .slide:last-of-type {
    opacity: 0;
  }
</style>

</style>