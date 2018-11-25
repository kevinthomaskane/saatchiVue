<template>
    <div :class="{ modal: true , show : show}">
        <div class="header">
            <div :class="[selectedTab === 'images' ? 'active' : '', 'images']" @click="selectedTab = 'images'">
                More Artwork
            </div>
            <div :class="[selectedTab === 'todos' ? 'active' : '', 'to-do']" @click="selectedTab = 'todos'">
                To-Do
            </div>

            <div :class="[selectedTab === 'bookmarks' ? 'active' : '', 'boookmarks']" @click="selectedTab = 'bookmarks'">
                Bookmarks
            </div>
            <div :class="[selectedTab === 'settings' ? 'active' : '', 'settings']" @click="selectedTab = 'settings'">
                Settings
            </div>
            <div class="close" @click="closeModal()">
                &times;
            </div>
        </div>
        <div v-if="selectedTab === 'images'" class="images-container">
            <h5 class="images-header">
                Choose a background
            </h5>
            <div class="row">
                <div v-for="(image, index) of images" :key="index" @click="setBg(image)" class="image" :data-info="JSON.stringify(image)" :style="'background-image: url(' + image.image_url + ')'">
                </div>
            </div>
        </div>
        <todo v-if="selectedTab === 'todos'" :todos="todos" :addToDo="addToDo" :deleteToDo="deleteToDo" />
        <bookmarks v-if="selectedTab === 'bookmarks'" />
        <settings v-if="selectedTab === 'settings'" 
        :artistSetting="artistSetting"
        :imageSetting="imageSetting"
        :searchSetting="searchSetting"
        :handleSetting="handleSetting"/>
    </div>
</template>

<script>
import ToDo from './ToDo'
import Bookmarks from './Bookmarks'
import Settings from './Settings'

import images from '@/constants/artwork'
export default {
  name: 'Modal',
  components: {
    todo: ToDo,
    bookmarks: Bookmarks,
    settings: Settings
  },
  props: {
    show: {
      type: Boolean,
      required: true
    },
    updateBg: {
      type: Function,
      required: true
    },
    closeModal: {
      type: Function,
      required: true
    },
    addToDo: {
      type: Function,
      required: true
    },
    deleteToDo: {
      type: Function,
      required: true
    },
    handleSetting: {
      type: Function,
      required: true
    },
    todos: {
      type: Array,
      required: true
    },
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
    }
  },
  data() {
    return {
      selectedTab: 'images',
      images: images
    }
  },
  methods: {
      setBg(image){
          this.handleSetting('image', false)
          this.updateBg(image)
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
      text-align: right;
    }
  }
  &.show {
    top: 50%;
  }
  .images-container {
    display: block;
    height: 398px;
    overflow-y: scroll;
    .images-header {
      font-size: 20px;
      font-weight: 200;
      text-align: center;
      padding: 30px;
    }
    .row {
      display: flex;
      justify-content: space-evenly;
      flex-wrap: wrap;
      .image {
        width: 45%;
        height: 200px;
        background-size: cover;
        margin-bottom: 20px;
        border-radius: 4px;
        box-shadow: 0 2px 2px gray;
        cursor: pointer;
      }
    }
  }
  .active {
    font-weight: bold;
  }
}
</style>
