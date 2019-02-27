<template>
  <div id="app">
    <side-screen
      :people="people"
      :side="'left'"
      :currentPage="0"
      @clickedPerson="showDrawer($event, 'left')"
      @currentSlide="left = $event">
    </side-screen>
    <side-drawer
      :drawerContent="drawerContent"
      class="left"
      ref="leftScreenDrawer">
    </side-drawer>

    <side-screen
      :people="people"
      :side="'right'"
      :currentPage="1"
      @clickedPerson="showDrawer($event, 'right')"
      @currentSlide="right = $event">
    </side-screen>
    <side-drawer
      :drawerContent="drawerContent"
      class="right"
      ref="rightScreenDrawer">
    </side-drawer>

    <div class="combo" @click="showMixDrawer">
      <p>Mix</p>
    </div>
    <side-drawer
      :drawerContent="mixContent"
      class="mix"
      ref="mixDrawer">
    </side-drawer>
  </div>
</template>

<script>
import sideScreen from './components/SideScreen.vue'
import sideDrawer from './components/SideDrawer.vue'

export default {
  name: 'app',
  components: { sideScreen, sideDrawer },
  data () {
    return {
      left: 0,
      right: 1,
      drawerIsOpen: false,
      drawerContent: {},
      mixContent: {},
      people: [
        {
          name: 'YongJun',
          color: '#DDDDDD',
          description: 'Senior Web Developer'
        },
        {
          name: 'Weixian',
          color: '#0074D9',
          description: 'AR and VR Specialist'
        },
        {
          name: 'MayLinn',
          color: '#7FDBFF',
          description: 'Drupal girl'
        },
        {
          name: 'Charles',
          color: '#2ECC40',
          description: 'Jimmy Neutron brought to life'
        },
        {
          name: 'Jocelyn',
          color: '#39CCCC',
          description: 'Free-spirited Junior'
        },
        {
          name: 'Sujin',
          color: '#FFDC00',
          description: 'Singapore Streets Expert'
        }
      ],
      relation: {
        'YongJun YongJun': 'Himself',
        'YongJun Weixian': 'Together they build up the code architecture for the team.',
        'YongJun MayLinn': 'Usually in discussions over premium stuff.',
        'YongJun Charles': 'Not yet collaborated.',
        'YongJun Jocelyn': 'The Vue Master and his young padawan.',
        'YongJun Sujin': 'Unfortunately separated by someone in between them.',
        'Weixian Weixian': 'Herself',
        'Weixian MayLinn': 'Best buddies',
        'Weixian Charles': 'Neighbours',
        'Weixian Jocelyn': 'Teammates',
        'Weixian Sujin': 'Teammates',
        'MayLinn MayLinn': 'Herself',
        'MayLinn Charles': 'Two ends of a row',
        'MayLinn Jocelyn': 'Initially trainer and trainee',
        'MayLinn Sujin': 'Workshop buddies',
        'Charles Charles': 'Himself',
        'Charles Jocelyn': 'Lunch mates',
        'Charles Sujin': 'Teammates',
        'Jocelyn Jocelyn': 'Herself',
        'Jocelyn Sujin': 'Neighbours',
        'Sujin Sujin': 'Herself'
      }
    }
  },
  methods: {
    showDrawer (person, side) {
      if (this.drawerIsOpen) {
        this.$refs[side + 'ScreenDrawer'].$el.classList.remove('slideIn')
        this.drawerIsOpen = false
      } else {
        this.drawerContent = person
        this.$refs[side + 'ScreenDrawer'].$el.classList.add('slideIn')
        this.drawerIsOpen = true
      }
    },
    showMixDrawer () {
      const name1 = this.people[this.left].name
      const name2 = this.people[this.right].name
      this.mixContent = {
        name: name1 + ' and ' + name2,
        description: this.relation[name1 + ' ' + name2] || this.relation[name2 + ' ' + name1]
      }
      this.$refs.mixDrawer.$el.classList.add('slideDown')
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
    z-index: 2;
    height: 200px;
    width: 200px;
    background-color: #333;
    border-radius: 50%;
    text-align: center;
    cursor: pointer;

    &:hover {
      background-color: #404040;
    }

    p {
      font-size: 20px;
      color: white;
    }
  }
}
</style>
