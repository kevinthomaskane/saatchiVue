<template>
    <div v-if="bookmarksArray.length > 0" class="bookmarks">
        <a v-for="(bookmark, index) of bookmarksArray" :key="index" :href="bookmark.url" class="bookmark-card">
            <img :src="'chrome://favicon/' + bookmark.url" alt="icon">
            <span>{{truncateTitle(bookmark.title)}}</span>
        </a>
    </div>
</template>

<script>
export default {
  name: 'Bookmarks',
  props: {},
  data() {
    return {
      bookmarksArray: []
    }
  },
  mounted() {
    chrome.bookmarks.getSubTree('0', data => {
      this.bookmarksArray = data[0].children[0].children
    })
  },
  methods: {
    truncateTitle(title) {
      let truncated = ''
      if (title.length > 35) {
        for (let i = 0; i < 35; i++) {
          truncated += title[i]
        }
        truncated += '...'
        return truncated
      }
      return title
    }
  }
}
</script>

<style lang="scss">
.bookmarks {
  height: 398px;
  overflow-y: scroll;
  display: flex;
  flex-wrap: wrap;
  padding: 15px;
  a {
    display: block;
    padding: 20px;
    color: black;
    margin: 5px;
    border-radius: 2px;
    box-shadow: 0 2px 2px rgba(0, 0, 0, 0.2);
    background-color: white;
    width: 18%;
    height: 100px;
    text-decoration: none;
    &:active {
      transform: translateY(1px);
      box-shadow: none;
    }
  }
  img {
    display: block;
    margin: 0 auto;
  }
  span {
    width: 100%;
    display: inline-block;
    text-align: center;
    margin-top: 5px;
  }
}
</style>
