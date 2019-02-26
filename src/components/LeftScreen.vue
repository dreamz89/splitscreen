<template>
  <div id="left">
    <div class="person" v-for="person in people" :style="{ height: fullHeight() }">
      <div class="name">
        {{ person.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['people'],
  methods: {
    fullHeight () {
      return window.innerHeight + 'px'
    }
  }
}
</script>

<style lang="scss">
#left {
  display: inline-block;
  height: 100%;
  width: 50%;

  .person {
    position: relative;

    .name {
      position: absolute;
      bottom: 0;
      left: 0;
      padding: 20px;
    }
  }
}
</style>
