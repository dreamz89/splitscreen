<template>
  <div class="drawer" ref="drawer">
    <div class="content">
      <h1>{{ drawerContent.name }}</h1>
      <p>{{ drawerContent.description }}</p>
    </div>
    <div class="close" @click="hideDrawer">
      X
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
          name: '',
          color: '',
          description: ''
        }
      }
    }
  },
  methods: {
    hideDrawer () {
      this.$refs.drawer.classList.remove('slideIn')
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
  left: 0;
  z-index: 2;
  background-color: white;
  transform: translateX(-100%);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 1s;

  .content {
    h1 {
      color: #333;
    }

    p {
      color: #333;
    }
  }

  .close {
    position: absolute;
    top: 0;
    right: 0;
    padding: 20px;
    font-size: 40px;
    cursor: pointer;
  }

  &.slideIn {
    transform: translateX(0);
  }
}
</style>
