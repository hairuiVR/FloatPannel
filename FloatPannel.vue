<template>
  <div class="floatingComponent" ref="floating" @touchstart="onStart" @touchmove="onMove" @touchend="onEnd">
    <div class="header">
      <div class="header-bar"></div>
    </div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'FloatPannel',
  data() {
    return {
      fLeft: 0, 
      fTop: 0,
      left: 0,
      top: 0,
    }
  },
  methods: {
    onStart(e) {
      this.fLeft = e.touches[0].clientX - this.$refs.floating.offsetLeft
      this.fTop = e.touches[0].clientY - this.$refs.floating.offsetTop
    },
    onMove(e) {
      const height = window.innerHeight
      let y = e.touches[0].clientY - this.fTop
      if (y > 200 && y < height - 200) {
        this.$refs.floating.style.top = y + 'px'
      }
    },
    onEnd(e) {},
  },
  mounted() {
    this.$refs.floating.style.top = 500 + 'px'
  },
}
</script>

<style lang="scss">
.floatingComponent {
  color: #ffff;
  position: fixed;
  z-index: 999;
  bottom: 0px;
  left: 0px;
  right: 0px;
  background: white;
  box-shadow: 0 0 5px 5px rgb(245, 241, 241);
  border-radius: 15px 15px 0px 0px;
  transition: transform 0.3s cubic-bezier(0.18, 0.89, 0.32, 1.28) 0s;
}
.header {
  width: 100%;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.header-bar {
  height: 5px;
  width: 30px;
  border-radius: var(--van-radius-md);
  background: #c8c9cc;
  border-radius: 4px;
}
</style>

