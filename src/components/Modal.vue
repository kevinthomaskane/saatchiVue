<template>
    <div :class="{ modal: true , show : show}">
        <div class="header">
            <div class="images">
                More Artwork
            </div>
            <div class="to-do">
                To-Do
            </div>

            <div class="bookmarks">
                Bookmarks
            </div>
            <div class="settings">
                Settings
            </div>
            <div class="close" @click="closeModal">
                &times;
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    show: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {}
  },
  methods: {
      closeModal(){
          this.$emit('closeModal')
      }
  }
}
</script>

<style lang="scss">
.modal {
  position: absolute;
  top: -1000px;
  width: 60%;
  height: 450px;
  border-radius: 2px;
  opacity: 1;
  transition: all 0.5s ease-in-out;
  z-index: 1000;
  left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  overflow: hidden;
  .header {
    height: 50px;
    background-color: #f05024;
    display: flex;
    text-align: center;
    justify-content: space-between;
    align-items: center;
    & > div {
      padding: 15px;
      display: inline-block;
      font-size: 16px;
      cursor: pointer;
      color: white;
      width: calc(100% / 5);
      font-weight: 200;
    }
  }
  &.show {
    top: 50%;
  }
}
</style>
