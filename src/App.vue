<template>
  <div id="app">
    <side-screen
      :people="people"
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
      :people="people"
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
import sideScreen from './components/SideScreen.vue'
import sideDrawer from './components/SideDrawer.vue'
import fullDrawer from './components/FullDrawer.vue'
import people from './data/people.json'
import relation from './data/relation.json'

export default {
  name: 'app',
  components: { sideScreen, sideDrawer, fullDrawer },
  data () {
    return {
      people,
      relation,
      left: 0,
      right: 1,
      drawerIsOpen: false,
      drawerContent: {},
      mixContent: {}
    }
  },
  methods: {
    toggleDrawer (person, side) {
      if (this.drawerIsOpen) {
        this.$refs[side + 'Drawer'].$el.classList.remove('slideIn')
      } else {
        this.drawerContent = person
        this.$refs[side + 'Drawer'].$el.classList.add('slideIn')
      }

      this.drawerIsOpen = !this.drawerIsOpen
      this.$refs.combo.classList.toggle('disabled')
    },
    toggleMixDrawer () {
      if (this.drawerIsOpen) {
        this.$refs.mixDrawer.$el.classList.remove('slideDown')
      } else {
        const name1 = this.people[this.left].name
        const name2 = this.people[this.right].name
        this.mixContent = this.relation[name1 + ' ' + name2] || this.relation[name2 + ' ' + name1]
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
    bottom: -100px;
    left: 50%;
    transform: translateX(-50%);
    z-index: 3;
    height: 200px;
    width: 200px;
    background-color: #333;
    border-radius: 50%;
    text-align: center;
    cursor: pointer;

    &:hover {
      background-color: #404040;
    }

    &.disabled {
      pointer-events: none;
      opacity: 0.8;
    }

    p {
      font-size: 20px;
      color: white;
    }
  }
}
</style>
