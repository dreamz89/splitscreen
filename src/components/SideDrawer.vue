<template>
  <div class="drawer">
    <div class="content">
      <h1>{{ drawerContent.breed }}</h1>
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
          breed: '',
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
  width: 50%;
  position: absolute;
  top: 0;
  z-index: 2;
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 1s;

  &.left {
    right: 0;
    transform: translateX(100%);
  }

  &.right {
    left: 0;
    transform: translateX(-100%);
  }

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

  &.slideIn {
    transform: translateX(0);
  }
}
</style>
