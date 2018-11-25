<template>
  <div id="app" v-if="vimg" :style="'background-image: url(' + vimg.image_url +')'">
    <searchBar v-if="vsearchSetting"/>
    <clock />
    <a class="saatchi-logo" href="https://www.saatchiart.com">
      <img src="./assets/sa-white.png" alt="saatchi logo">
    </a>
    <a href="#" class="add-note" @click="createNote">
      Add a note <span>+</span>
    </a>
    <div class="notes">
      <note v-if="vnotes.length > 0" v-for="(item, index) of vnotes" :currentNote="item" @saveNote="saveNote" @deleteNote="deleteNote" :key="index"/>
    </div>
    <card v-if="vimg && vartistSetting" :image="vimg"/>
    <settingsBtn :modalOpen="modalOpen" @openModal="openModal"/>
    <modal :show="modalOpen" 
    :closeModal="closeModal" 
    :addToDo="addToDo" 
    :updateBg="updateBg" 
    :todos="vtodos" 
    :deleteToDo="deleteToDo" 
    :artistSetting="vartistSetting"
    :imageSetting="vimageSetting"
    :searchSetting="vsearchSetting"
    :handleSetting="handleSetting" />
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue'
import Clock from './components/Clock.vue'
import Note from './components/Note.vue'
import Card from './components/Card.vue'
import SettingsBtn from './components/SettingsBtn.vue'
import Modal from './components/Modal.vue'

import images from '@/constants/artwork'

export default {
  name: 'app',
  components: {
    searchBar: SearchBar,
    clock: Clock,
    note: Note,
    settingsBtn: SettingsBtn,
    card: Card,
    modal: Modal
  },
  data() {
    return {
      vimg: {},
      vartistSetting: true,
      vimageSetting: true,
      vsearchSetting: true,
      vtodos: [],
      vnotes: [],
      modalOpen: false
    }
  },
  mounted() {
    this.setStorage(this.$data)
    this.renderBg()
  },
  methods: {
    setStorage(obj) {
      for (let prop in obj) {
        if (localStorage.getItem(prop)) {
          this.$data[prop] = JSON.parse(localStorage.getItem(prop))
        } else {
          localStorage.setItem(prop, JSON.stringify(obj[prop]))
        }
      }
    },
    renderBg() {
      if (this.vimageSetting) {
        const randomIndex = Math.floor(Math.random() * images.length)
        this.vimg = images[randomIndex]
        localStorage.setItem('vimg', JSON.stringify(this.vimg))
      }
    },
    handleSetting(x, bool) {
      if (x === 'image') {
        localStorage.setItem('vimageSetting', JSON.stringify(bool))
        this.vimageSetting = bool
        return
      }
      if (x === 'artist') {
        localStorage.setItem('vartistSetting', JSON.stringify(bool))
        this.vartistSetting = bool
        return
      }
      if (x === 'search') {
        localStorage.setItem('vsearchSetting', JSON.stringify(bool))
        this.vsearchSetting = bool
      }
    },
    openModal() {
      this.modalOpen = true
    },
    closeModal() {
      this.modalOpen = false
    },
    updateBg(image) {
      localStorage.setItem('vimg', JSON.stringify(image))
      this.vimg = image
    },
    addToDo(content) {
      this.vtodos.unshift({ id: Math.random(), content: content })
      localStorage.setItem('vtodos', JSON.stringify(this.vtodos))
    },
    deleteToDo(item) {
      const newArr = this.vtodos.filter(el => el.id != item)
      localStorage.setItem('vtodos', JSON.stringify(newArr))
      this.vtodos = newArr
    },
    createNote() {
      this.vnotes.unshift({ id: Math.random(), text: '' })
    },
    saveNote(newNote) {
      for (let i = 0; i < this.vnotes.length; i++) {
        if (this.vnotes[i].id === newNote.id) {
          this.vnotes[i].text = newNote.text
          localStorage.setItem('vnotes', JSON.stringify(this.vnotes))
          return
        }
      }
    },
    deleteNote(note) {
      const arr = this.vnotes.filter(el => el.id != note.id)
      localStorage.setItem('vnotes', JSON.stringify(arr))
      this.vnotes = arr
    }
  }
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  margin: 0;
  padding: 0;
  max-width: 100%;
  width: 100%;
  height: 100%;
  max-height: 100%;
}

body {
  position: relative;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  font-family: "Helvetica", sans-serif;
}

input,
textarea {
  outline: none;
  resize: none;
  &:focus {
    outline: none;
  }
}

#app {
  width: 100vw;
  height: 100vh;
  background-size: cover;
  background-position: center;
  .saatchi-logo {
    position: fixed;
    top: 10px;
    left: 10px;
    padding: 10px;
    padding-top: 15px;
    img {
      width: 200px;
    }
  }
  .add-note {
    display: inline-block;
    padding: 8px;
    color: white;
    border-radius: 5px;
    text-align: right;
    text-decoration: none;
    margin-bottom: 10px;
    text-shadow: 1px 2px 1px rgba(0, 0, 0, 0.5);
    font-size: 14px;
    display: block;
    position: fixed;
    top: 35px;
    right: 10px;
  }
  .notes {
    height: auto;
    max-height: 80vh;
    overflow: auto;
    width: auto;
    position: fixed;
    top: 70px;
    right: 10px;
  }
}
</style>
