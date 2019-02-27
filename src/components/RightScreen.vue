<template>
  <div id="right">
    <slider ref="slider" :options="options">
      <slideritem
        class="person"
        v-for="(person, index) in people"
        :key="index"
        :style="{ backgroundColor: person.color, height: fullHeight() }">
        <div class="name" @click="$emit('clickedPerson', person)">
          {{ person.name }} →
        </div>
      </slideritem>
    </slider>
  </div>
</template>

<script>
import { slider, slideritem } from 'vue-concise-slider' // https://warpcgd.github.io/vue-concise-slider/

export default {
  props: ['people'],
  components: { slider, slideritem },
  data() {
    return {
      fire: true,
      timer: null,
      options: {
        direction: 'vertical',
        slidesToScroll: 1,
        currentPage: 1,
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
    slide () {
      this.$refs.slider.$emit('slidePre')
    },
    slideNext () {
      this.$refs.slider.$emit('slideNext')
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
          this.slide()
          this.fire = false
        }
      }
    },
  }
}
</script>

<style lang="scss">
#right {
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
