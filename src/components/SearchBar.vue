<template>
    <div class="search">
        <input type="text" :value="query" @keyup.enter="handleSubmit" @input="handleChange" placeholder="Google Search..." class="search-bar">
    </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data() {
    return {
      query: ''
    }
  },
  methods: {
    handleChange(e){
      this.query = e.target.value
    },
    handleSubmit(){
      if (this.query.length >= 1){
        const query = this.query.trim().split(" ").join("+")
        this.query = ''
        window.location.href = `https://www.google.com/search?q=${query}`
      }
    }
  }
}
</script>

<style lang="scss">
.search {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  .search-bar {
    width: 584px;
    border-radius: 2px;
    background-color: white;
    box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.16);
    height: 44px;
    padding-left: 15px;
    font-family: 'Helvetica', sans-serif;
    font-size: 16px;
    border: none;
    &:focus {
      outline: transparent;
      box-shadow: 0 3px 3px 0 rgba(0, 0, 0, 0.16);
      &::placeholder {
        opacity: 0;
      }
    }
    &::placeholder {
      text-align: center;
    }
  }
}
</style>
