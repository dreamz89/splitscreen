<template>
  <div class="side">
    <slider ref="slider" :options="options" @slide='slide'>
      <slideritem
        v-for="(breed, index) in breeds"
        :key="index"
        :style="{
          backgroundImage: 'url(' + require('@/assets/' + breed.image) + ')',
          height: fullHeight()
        }">
        <div class="overlay"
          @wheel="handleScroll"
          @mousedown="handleDown"
          @mouseup="handleUp($event, breed)"
        ></div>
      </slideritem>
    </slider>
  </div>
</template>

<script>
import { slider, slideritem } from 'vue-concise-slider' // https://warpcgd.github.io/vue-concise-slider/

export default {
  props: ['breeds', 'currentPage', 'side'],
  components: { slider, slideritem },
  data() {
    return {
      scrollable: true,
      initialPosition: null,
      finalPosition: null,
      timer: null,
      options: {
        direction: 'vertical',
        slidesToScroll: 1,
        currentPage: this.currentPage,
        loop: true,
        pagination: false
      }
    }
  },
  methods: {
    fullHeight () {
      return window.innerHeight + 'px'
    },
    slidePre () {
      this.$refs.slider.$emit('slidePre')
    },
    slideNext () {
      this.$refs.slider.$emit('slideNext')
    },
    slide (data) {
      this.$emit('currentSlide', data.currentPage)
    },
    handleScroll (e) {
      e.preventDefault()

      if (this.timer !== null) {
        clearTimeout(this.timer)
      }

      this.timer = setTimeout(() => {
        this.scrollable = true
      }, 50)

      if (this.scrollable) {
        if (e.deltaY < 0) {
          this.slideNext()
          this.scrollable = false
        } else {
          this.slidePre()
          this.scrollable = false
        }
      }
    },
    handleDown (e) {
      this.initialPosition = e.pageX + e.pageY
    },
    handleUp (e, breed) {
      const finalPosition = e.pageX + e.pageY
      const difference = finalPosition - this.initialPosition
      if (Math.abs(difference) < 10) this.$emit('chosen', breed)
    }
  }
}
</script>

<style lang="scss">
.side {
  display: inline-block;
  width: 50%;
  vertical-align: top;

  .slider-item {
    background-size: cover;
    background-repeat: no-repeat;

    .overlay {
      height: 100%;
      width: 100%;
      cursor: pointer;
    }
  }
}
</style>
