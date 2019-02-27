<template>
  <div id="app">
    <left-screen :people="people" @clickedPerson="showDrawer($event)"></left-screen>
    <left-screen-drawer :drawerContent="drawerContent" ref="leftScreenDrawer"></left-screen-drawer>

    <right-screen :people="people"></right-screen>
  </div>
</template>

<script>
import leftScreen from './components/LeftScreen.vue'
import leftScreenDrawer from './components/LeftScreenDrawer.vue'

import rightScreen from './components/RightScreen.vue'

export default {
  name: 'app',
  components: { leftScreen, leftScreenDrawer, rightScreen },
  data () {
    return {
      left: '',
      right: '',
      drawerContent: {},
      people: [
        {
          name: 'YongJun',
          color: '#DDDDDD',
          description: 'Senior Web Developer'
        },
        {
          name: 'WeiXian',
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
      relation: [
        {
          pair: ['YongJun', 'Weixian'],
          description: 'Together they build up the code architecture for the team.'
        },
        {
          pair: ['YongJun', 'MayLinn'],
          description: 'Usually in discussions over premium stuff.'
        },
        {
          pair: ['YongJun', 'Charles'],
          description: 'Not yet collaborated.'
        },
        {
          pair: ['YongJun', 'Jocelyn'],
          description: 'The Vue Master and his young padawan.'
        },
        {
          pair: ['YongJun', 'Sujin'],
          description: 'Unfortunately separated by someone in between them.'
        }
      ]
    }
  },
  methods: {
    showDrawer(person) {
      this.drawerContent = person
      this.$refs.leftScreenDrawer.$el.classList.add('slideIn')
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
}
</style>
