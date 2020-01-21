<template>
  <div class="drawer">
    <div class="content">
      <img :src="'./assets/' + this.drawerContent.mobileImage"/>
      <h1>{{ drawerContent.name }}</h1>
      <p>{{ drawerContent.description }}</p>
    </div>
    <div class="close" @click="$emit('chosen')">
      &times;
    </div>
  </div>
</template>

<script>
export default {
  props: {
    drawerContent: {
      type: Object,
      required: true,
      default: function() {
        return {
          description: ''
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.drawer {
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  transform: translateY(-100%);
  z-index: 2;
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 1s;

  .content {
    padding: 20px;

    h1 {
      font-family: 'Libre Baskerville', serif;
      color: #333;
    }

    p {
      font-family: 'Open Sans', sans-serif;
      color: #333;
    }
  }

  .close {
    position: absolute;
    top: 0;
    right: 0;
    padding: 20px;
    font-size: 40px;
    line-height: 0.6em;
    cursor: pointer;
  }

  &.slideDown {
    transform: translateY(0);
  }
}
</style>
