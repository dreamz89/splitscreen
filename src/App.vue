<template>
  <div id="app">
    <left-screen :people="people"></left-screen>
    <right-screen :people="people"></right-screen>
  </div>
</template>

<script>
import LeftScreen from './components/LeftScreen.vue'
import RightScreen from './components/RightScreen.vue'

export default {
  name: 'app',
  components: { LeftScreen, RightScreen },
  data () {
    return {
      left: '',
      right: '',
      people: [
        {
          name: 'YongJun',
          color: '#001f3f',
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
