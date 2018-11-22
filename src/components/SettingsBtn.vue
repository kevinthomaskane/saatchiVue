<template>
    <a class="settingsBtn" href="#" @click="handleClick">
        <span class="dot"></span>
    </a>
</template>

<script>
export default {
  name: 'SettingsBtn',
  data() {
    return {}
  },
  props: {
    modalOpen: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    handleClick() {
      if (!this.modalOpen) {
        this.$emit('openModal')
      }
    }
  }
}
</script>

<style lang="scss">
.settingsBtn {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.8);
  position: fixed;
  bottom: 15px;
  right: 15px;
  .dot {
    display: block;
    width: 5px;
    height: 5px;
    margin: 23px auto 0 auto;
    background-color: black;
    border-radius: 50%;
    position: relative;
    &:before {
      content: '';
      width: 5px;
      height: 5px;
      background-color: black;
      border-radius: 50%;
      position: absolute;
      left: -10px;
      top: 0;
    }
    &:after {
      content: '';
      width: 5px;
      height: 5px;
      background-color: black;
      border-radius: 50%;
      position: absolute;
      right: -10px;
      top: 0;
    }
  }
}
</style>
