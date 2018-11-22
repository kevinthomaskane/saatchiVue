<template>
    <div class="note">
      <div class="delete" @click="deleteNote">&times;</div>
      <textarea class="text" @input="handleChange" :value="text"></textarea>
    </div>
</template>

<script>
export default {
  name: 'Note',
  props: {
    currentNote: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      text: this.currentNote.text
    }
  },
  watch: {
    currentNote(){
      this.text = this.currentNote.text
    }
  },
  methods: {
    handleChange(e) {
      this.text = e.target.value
      this.currentNote.text = e.target.value
      this.$emit('saveNote', this.currentNote)
    },
    deleteNote(){
      this.$emit('deleteNote', this.currentNote)
    }
  }
}
</script>

<style lang="scss">
.note {
  width: 200px;
  height: 200px;
  position: relative;
  background: rgb(248, 248, 96);
  overflow: hidden;
  margin-bottom: 5px;
  .delete {
    position: absolute;
    top: 5px;
    right: 8px;
    cursor: pointer;
    font-size: 16px;
  }
  .text {
    width: 180px;
    height: 180px;
    background: transparent;
    outline: none;
    font-size: 14px;
    color: inherit;
    resize: none;
    border: none;
    margin-top: 20px;
    margin-left: 10px;
  }
}
</style>
