<template>
  <div id="app">
    <side-screen
      :breeds="breeds"
      :side="'left'"
      :currentPage="0"
      @chosen="toggleDrawer($event, 'left')"
      @currentSlide="left = $event"
    ></side-screen>
    <side-drawer
      :drawerContent="drawerContent"
      class="left"
      ref="leftDrawer"
      @chosen="toggleDrawer($event, 'left')"
    ></side-drawer>

    <side-screen
      :breeds="breeds"
      :side="'right'"
      :currentPage="1"
      @chosen="toggleDrawer($event, 'right')"
      @currentSlide="right = $event"
    ></side-screen>
    <side-drawer
      :drawerContent="drawerContent"
      class="right"
      ref="rightDrawer"
      @chosen="toggleDrawer($event, 'right')"
    ></side-drawer>

    <div class="combo" ref="combo" @click="toggleMixDrawer">
      <p>Mix</p>
    </div>
    <full-drawer
      :drawerContent="mixContent"
      ref="mixDrawer"
      @chosen="toggleMixDrawer"
    ></full-drawer>
  </div>
</template>

<script>
import SideScreen from './components/SideScreen.vue'
import SideDrawer from './components/SideDrawer.vue'
import FullDrawer from './components/FullDrawer.vue'
import breeds from './data/breeds.json'
import mixes from './data/mixes.json'

export default {
  name: 'app',
  components: { SideScreen, SideDrawer, FullDrawer },
  data () {
    return {
      breeds,
      mixes,
      left: 0,
      right: 1,
      drawerIsOpen: false,
      drawerContent: {},
      mixContent: {}
    }
  },
  methods: {
    toggleDrawer (breed, side) {
      if (this.drawerIsOpen) {
        this.$refs[side + 'Drawer'].$el.classList.remove('slideIn')
      } else {
        this.drawerContent = breed
        this.$refs[side + 'Drawer'].$el.classList.add('slideIn')
      }

      this.drawerIsOpen = !this.drawerIsOpen
      this.$refs.combo.classList.toggle('disabled')
    },
    toggleMixDrawer () {
      if (this.drawerIsOpen) {
        this.$refs.mixDrawer.$el.classList.remove('slideDown')
      } else {
        const breed1 = this.breeds[this.left].breed
        const breed2 = this.breeds[this.right].breed

        this.mixContent = this.mixes[breed1 + ' ' + breed2] || this.mixes[breed2 + ' ' + breed1]
        this.$refs.mixDrawer.$el.classList.add('slideDown')
      }

      this.drawerIsOpen = !this.drawerIsOpen
    }
  }
}
</script>

<style lang="scss">
html, body {
  height: 100%;
  margin: 0;
  overflow: hidden;
}
#app {
  height: 100%;
  position: relative;

  .combo {
    position: absolute;
    bottom: -25vw;
    left: 50%;
    transform: translateX(-50%);
    z-index: 3;
    height: 50vw;
    width: 50vw;
    max-height: 200px;
    max-width: 200px;
    background-color: #333;
    border-radius: 50%;
    text-align: center;
    cursor: pointer;

    @media (min-width: 400px) {
      bottom: -100px;
    }

    &:hover {
      background-color: #404040;
    }

    &.disabled {
      z-index: 0;
      opacity: 0;
      transition: opacity 0.5s;
    }

    p {
      font-size: 20px;
      color: white;
    }
  }
}
</style>
