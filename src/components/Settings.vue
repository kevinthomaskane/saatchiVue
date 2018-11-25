<template>
    <div class="settings">
        <div class="settings-item">
            <div class="remove-search">
                Show search bar
            </div>
            <div class="slider-container">
                <div class="no" @click="handleSetting('search', false)"></div>
                <div class="yes" @click="handleSetting('search', true)"></div>
                <div :class="[searchSetting ? 'true' : 'false', 'slide']"></div>
            </div>
        </div>
        <div class="settings-item">
            <div class="remove-search">
                New artwork every time
            </div>
            <div class="slider-container">
                <div class="no" @click="handleSetting('image', false)"></div>
                <div class="yes" @click="handleSetting('image', true)"></div>
                <div :class="[imageSetting ? 'true' : 'false', 'slide']"></div>
            </div>
        </div>
        <div class="settings-item">
            <div class="remove-artist">
                Show artist card
            </div>
            <div class="slider-container">
                <div class="no" @click="handleSetting('artist', false)"></div>
                <div class="yes" @click="handleSetting('artist', true)"></div>
                <div :class="[artistSetting ? 'true' : 'false', 'slide']"></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Settings',
  props: {
    artistSetting: {
      type: Boolean,
      required: true
    },
    searchSetting: {
      type: Boolean,
      required: true
    },
    imageSetting: {
      type: Boolean,
      required: true
    },
    handleSetting: {
      type: Function,
      required: true
    }
  },
  data() {
    return {}
  },
  methods: {}
}
</script>

<style lang="scss">
.settings {
  padding-top: 130px;
  .settings-item {
    display: flex;
    justify-content: space-between;
    width: 300px;
    margin: 0 auto 20px auto;
    font-size: 16px;
    .slider-container {
      width: 50px;
      height: 20px;
      display: flex;
      position: relative;
      border: solid 1px #dbdbdb;
      border-radius: 10px;
      box-shadow: inset 0 0 10px #cccccc;
      .yes {
        width: 50%;
        height: 100%;
        background: transparent;
        cursor: pointer;
      }
      .no {
        width: 50%;
        height: 100%;
        background: transparent;
        cursor: pointer;
      }
      .slide {
        position: absolute;
        width: 25px;
        height: 25px;
        top: -2px;
        right: -1px;
        background: #f05024;
        transition: right 0.2s ease-in-out;
        border-radius: 50%;
        box-shadow: -2px 0px 8px 2px #dbdbdb;
        cursor: pointer;
        &.true {
          right: -1px;
          background: #f05024;
          box-shadow: -2px 0px 8px 2px #dbdbdb;
        }
        &.false {
          right: 26px;
          background: gray;
          box-shadow: 2px 0px 8px 2px #dbdbdb;
        }
      }
    }
  }
}
</style>
