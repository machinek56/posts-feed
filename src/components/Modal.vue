<template>
  <div>
    <div class="modal__overlay"></div>
    <div class="modal__container">
      <div class="modal__body">
        <button class="modal__close" @click="close" title="close">&times;</button>

        <slot></slot>

      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Modal',
  methods: {
    close () {
      this.$emit('close')
    }
  }
}
</script>

<style scoped>
  .modal__overlay {
    position: fixed;
    z-index: 999;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: .5;
    background-color: #000;
    transition: opacity .3s ease;
  }

  .modal__container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow-y: auto;
    z-index: 1000;
  }

  .modal__body {
    width: 700px;
    margin: 40px auto;
    padding: 20px 30px;
    background-color: #fff;
    border-radius: 2px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
    position: relative;
  }

  .modal__close {
    position: absolute;
    right: 20px;
    top: 20px;
    border: 0;
    font-size: 30px;
    cursor: pointer;
  }
</style>
