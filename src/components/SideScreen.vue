<template>
  <div class="side">
    <slider ref="slider" :options="options" @slide='slide'>
      <slideritem
        class="person"
        v-for="(person, index) in people"
        :key="index"
        :style="{ backgroundColor: person.color, height: fullHeight() }">
        <div class="name" @click="$emit('chosen', person)">
          {{ side === 'left' ? person.name + ' →' : '← ' + person.name }}
        </div>
      </slideritem>
    </slider>
  </div>
</template>

<script>
import { slider, slideritem } from 'vue-concise-slider' // https://warpcgd.github.io/vue-concise-slider/

export default {
  props: ['people', 'currentPage', 'side'],
  components: { slider, slideritem },
  data() {
    return {
      fire: true,
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
  mounted () {
    this.$refs.slider.$el.addEventListener('wheel', this.handleScroll)
  },
  destroyed () {
    this.$refs.slider.$el.removeEventListener('wheel', this.handleScroll)
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
        this.fire = true
      }, 50)

      if (this.fire) {
        if (e.deltaY < 0) {
          this.slideNext()
          this.fire = false
        } else {
          this.slidePre()
          this.fire = false
        }
      }
    },
  }
}
</script>

<style lang="scss">
.side {
  display: inline-block;
  width: 50%;
  vertical-align: top;

  .person {
    overflow: auto;

    .name {
      font-size: 20px;
      cursor: pointer;
    }
  }
}
</style>