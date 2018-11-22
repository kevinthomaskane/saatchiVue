<template>
  <div id="app" v-if="vimg" :style="'background-image: url(' + vimg.image_url +')'">
    <searchBar/>
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
    <card v-if="vimg" :image="vimg"/>
    <settingsBtn :modalOpen="modalOpen" @openModal="openModal"/>
    <modal :show="modalOpen" @closeModal="closeModal" />
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
      vartistSetting: false,
      vimageSetting: false,
      vsearchSetting: false,
      todos: {},
      vnotes: [],
      modalOpen: false
    }
  },
  mounted() {
    this.renderComponents()
  },
  methods: {
    openModal(){
      this.modalOpen = true
    },
    closeModal(){
      this.modalOpen = false
    },
    renderComponents() {
      this.vimg = this.getBgImage()
      this.vartistSetting = this.getArtistSetting()
      this.vimageSetting = this.getImageSetting()
      this.vsearchSetting = this.getSearchSetting()
      this.vtodos = this.getTodos()
      this.vnotes = this.getNotes()
    },
    getBgImage() {
      const randomIndex = Math.floor(Math.random() * images.length)
      this.vimg = images[randomIndex]
      return this.setLocalStorage('vimg', this.vimg)
    },
    getArtistSetting() {
      return this.setLocalStorage('vartistSetting', false)
    },
    getImageSetting() {
      return this.setLocalStorage('vimageSetting', false)
    },
    getSearchSetting() {
      return this.setLocalStorage('vsearchSetting', false)
    },
    getTodos() {
      return this.setLocalStorage('vtodos', {})
    },
    getNotes() {
      return this.setLocalStorage('vnotes', [])
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
      const arr = this.vnotes.filter(el => {
        return el.id !== note.id
      })
      localStorage.setItem('vnotes', JSON.stringify(arr))
      this.vnotes = arr
    },
    setLocalStorage(key, type) {
      if (this.checkIfEmpty(JSON.parse(localStorage.getItem(key)))) {
        localStorage.setItem(key, JSON.stringify(type))
        return type
      } else {
        return JSON.parse(localStorage.getItem(key))
      }
    },
    checkIfEmpty(n) {
      if (n === null || n === undefined) {
        return true
      }
      if (typeof n === 'boolean') {
        return n
      }
      if (typeof n === 'object') {
        if (Object.keys(n).length === 0) {
          return true
        }
      }
      if (n.length === 0) {
        return true
      }
      return false
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
