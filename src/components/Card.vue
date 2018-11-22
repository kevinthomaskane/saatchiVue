<template>
    <div class="card">
        <div class="container">
            <div class="title">{{image.title}}</div>
            <div class="artist-name">{{image.artist}}</div>
            <a class="saatchi-link" :href="image.url">View on saatchiart.com</a>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    image: {
      type: Object,
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
.card {
  position: fixed;
  bottom: 15px;
  left: 15px;
  width: auto;
  max-width: 350px;
  height: auto;
  .container {
    color: white;
    height: calc(100% - 30px);
    padding: 15px;
    position: relative;
    border-radius: 4px;
    text-shadow: 1px 2px 1px rgba(0, 0, 0, 0.5);
    .title {
      font-weight: bold;
      font-size: 14px;
      font-style: italic;
      margin-bottom: 5px;
    }
    .artist-name {
      font-size: 14px;
      margin-bottom: 5px;
    }
    .saatchi-link {
      color: white;
      font-size: 14px;
      text-shadow: 1px 2px 1px rgba(0, 0, 0, 0.5);
      text-decoration: none;
    }
  }
}
</style>
