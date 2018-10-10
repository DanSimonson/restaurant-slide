<template>
  <div class='carousel-view '>
    <div class='button-prev' @click="arrowLeft" name='fade'></div>
    <transition-group class='carousel' tag="div">
      <div v-for="(slide, index) in slides" class='slide' :key="slide.id" :style="{backgroundImage: 'url(' + slides[index].imgLink + ')'}">
        <!--<img :src='slide.imgLink'>-->
        <h4> {{ slide.title }} </h4>
      </div>
    </transition-group>

    <div class='carousel-controls'>
      <div class='squares'>
        <div v-for="(slide, index) in slides" :key="slide.id" :style="{backgroundImage: 'url(' + slides[index].imgLink + ')'}">
          <!--<h4 style="color:black">{{slide.title}}</h4>-->
        </div>
        <p style="display:inline-block;">{{ slides[currentMsg].title }}</p>

      </div>
      <!--<button class='carousel-controls__button' @click="previous">prev</button>
      <button class='carousel-controls__button' @click="next">next</button>-->

    </div>
    <div class='button-next' @click="arrowRight"></div>
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
        ],
        stopMe: null,
        stopMsg: null,
        currentMsg: ''
      }
    },
    created() {
      let selfie = this;
      this.stopMe = setInterval(() => {
        selfie.next();
      }, 4000)
      this.stopMsg = setTimeout(() => {
        this.nextSlide();
      }, 4000)
      this.nextSlide()

    },
    methods: {
      nextSlide() {
        if (this.currentMsg + 1 < this.slides.length) {
          this.currentMsg++;
        } else {
          this.currentMsg = 0
        }
      },
      next() {
        const first = this.slides.shift()
        this.slides = this.slides.concat(first)
      },
      previous() {
        const last = this.slides.pop()
        this.slides = [last].concat(this.slides)
      },
      arrowLeft() {
        clearInterval(this.stopMe);
        this.previous();
        let selfie = this;
        this.stopMe = setInterval(() => {
          selfie.previous()
        }, 4000)

      },
      arrowRight() {
        clearInterval(this.stopMe);
        this.next();
        let selfie = this;
        this.stopMe = setInterval(() => {
          selfie.next()
        }, 4000)
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h4 {
    color: #fff;
  }

  .flex1 {
    flex: 1 1 20em;
  }

  .flex2 {
    flex: 2 2 20em;
  }

  .carousel-view {
    position: relative;
    width: 400px;
  }

  .carousel-view .button-prev,
  .carousel-view .button-next {
    /*height: 20px;
    width: 20px;
    background-color: yellow;*/
    position: absolute;
    top: 50%;
    border: 12px solid transparent;

    /*border-left-color: transparent;
    border-right-color: purple;
    border-bottom-color: violet;
    border-top-color: crimson;
    */
  }

  .carousel-view .button-prev {
    border-right-color: black;
    transform: rotate(-3deg)
  }


  .carousel-view .button-next {
    border-left-color: black;
    transform: rotate(3deg);
  }

  .carousel-controls .squares {
    position: absolute;
    bottom: 0;
  }

  .carousel-controls .squares div {

    /*height: 20px;
    width: 20px;    
    margin-right: 10px;
    background-color: yellow;
    border-radius: 50%;
    display: flex;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);*/

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
    border: 0.1em solid #000;
    border-radius: 50%;
    transition: transform 0.3s ease-in-out;

  }

  .slide:first-of-type {
    opacity: 0;
  }

  .slide:last-of-type {
    opacity: 0;
  }

  .fade-enter-active,
  .fade-leave-active {
    transition: all 0.8s ease;
    overflow: hidden;
    visibility: visible;
    opacity: 1;
    position: absolute;
  }

  .fade-enter,
  .fade-leave-to {
    opacity: 0;
    visibility: hidden;
  }

  /*media queries*/
  @media screen and (max-width: 320px) {
    .slide {
      height: 21em;
      flex: 0 0 21em;
    }

    .carousel-view .button-next {
      right: 3%;
      padding: 2px;
    }

    .carousel-view .button-prev {}

    .carousel-controls .squares {

      left: 30%;
    }


  }

  @media screen and (max-width: 375px) {
    .slide {
      height: 20em;
      flex: 0 0 20em;
    }

    .carousel-view .button-next {
      right: 3%;
      padding: 2px;
    }

    .carousel-view .button-prev {}

    .carousel-controls .squares {

      left: 30%;
    }
  }

  @media screen and (max-width: 425px) {
    .slide {
      height: 20em;
      flex: 0 0 20em;
    }

    .carousel-view .button-next {
      right: 3%;
      padding: 2px;
    }

    .carousel-view .button-prev {}

    .carousel-controls .squares {

      left: 30%;
    }
  }

  @media screen and (max-width: 768px) {
    .slide {
      height: 20em;
      flex: 0 0 20em;
    }

    .carousel-view .button-next {
      right: 3%;
      padding: 2px;
    }

    .carousel-view .button-prev {}

    .carousel-controls .squares {

      left: 30%;
    }
  }

  @media screen and (max-width: 1024px) {
    .slide {
      height: 20em;
      flex: 0 0 20em;
    }

    .carousel-view .button-next {
      right: 3%;
      padding: 2px;
    }

    .carousel-view .button-prev {}

    .carousel-controls .squares {
      left: 30%;
    }
  }

  @media screen and (max-width: 1440px) {
    .slide {
      height: 20em;
      flex: 0 0 20em;
    }

    .carousel-view .button-next {
      right: 3%;
      padding: 2px;
    }

    .carousel-view .button-prev {}

    .carousel-controls .squares {
      left: 30%;
    }
  }

  @media screen and (max-width: 2560px) {
    .slide {
      height: 20em;
      flex: 0 0 20em;
    }

    .carousel-view .button-next {
      right: 3%;
      padding: 2px;
    }

    .carousel-view .button-prev {}

    .carousel-controls .squares {
      left: 30%;
    }
  }
</style>