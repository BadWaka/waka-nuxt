<template>
  <section
    class="modal-wrapper"
    @click.self="handleClose">
    <section class="modal">
      <i
        class="el-icon-close c-btn c-font-20 transition-animate"
        @click.stop="handleClose">
      </i>
      <slot></slot>
    </section>
  </section>
</template>

<script>
  export default {
    name: 'Modal',
    data() {
      return {}
    },
    methods: {
      handleClose() {
        this.$emit('close');
      }
    }
  }
</script>

<style lang="scss" scoped>
  @import "../assets/app.scss";

  .modal-wrapper {
    position: fixed;
    top: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100vw;
    height: 100vh;
    z-index: 99;
    background: $primaryColor50;

    .modal {
      position: relative;
      background: #fff;
      padding: 40px;
      box-sizing: border-box;

      .el-icon-close {
        position: absolute;
        right: 10px;
        top: 10px;

        &:hover {
          transform: rotate(90deg);
        }
      }
    }
  }

</style>
