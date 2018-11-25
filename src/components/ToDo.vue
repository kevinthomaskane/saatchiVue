<template>
    <div class="todo">
       <div class="input-container">
            <input type="text" class="input" :value="newItem" @input="handleInput" @keypress.enter="addToDo(newItem)" placeholder="add an item">
            <a href="#" class="add" @click="addToDo(newItem)">&#43;</a>
        </div>
        <h5>My items</h5>
        <div v-if="Object.keys(todos).length < 1" class="placeholder">
            No Items...
        </div>
        <ul>
            <li v-for="(item, index) of todos" :key="index" :data-id="item.id">
                {{item.content}}
                <div class="trash" @click="deleteToDo(item.id)">&#128465;</div>
            </li>
        </ul>
    </div>
</template>

<script>
import images from '@/constants/artwork'
export default {
  name: 'Todo',
  components: {},
  props: {
    todos: {
      type: Array,
      required: true
    },
    addToDo: {
      type: Function,
      required: true
    },
    deleteToDo: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      newItem: ''
    }
  },
  methods: {
    handleInput(e) {
      this.newItem = e.target.value
    }
  }
}
</script>

<style lang="scss">
.todo {
  text-align: center;
  position: relative;
  width: 450px;
  margin: 0 auto;
  height: 360px;
  .placeholder {
    font-size: 20px;
    padding: 90px;
    color: #f05024;
    font-weight: 200;
  }
  h5 {
    font-size: 20px;
    margin: 15px 0;
    font-weight: 200;
  }
  .input-container {
    position: relative;
    width: 400px;
    height: 50px;
    box-sizing: border-box;
    margin: 40px auto 0;
    input {
      width: 100%;
      height: 100%;
      padding-right: 45px;
      padding-left: 10px;
      font-size: 16px;
      color: inherit;
      border: solid 1px rgb(231, 231, 231);
      border-radius: 2px;
      box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.16);
      transition: all 0.2s ease-in-out;
      box-sizing: border-box;
    }
    .add {
      position: absolute;
      right: 0;
      top: 0;
      width: 40px;
      height: 100%;
      background-color: #f05024;
      border-radius: 0 2px 2px 0;
      padding-top: 12px;
      font-size: 20px;
      text-decoration: none;
      color: white;
      box-sizing: border-box;
    }
  }
  ul {
    list-style: none;
    text-align: left;
    padding-left: 0;
    height: 229px;
    max-height: 229px;
    overflow-y: scroll;
    li {
      padding: 15px;
      padding-right: 50px;
      position: relative;
      background-color: white;
      border-bottom: solid 1px rgb(236, 236, 236);
      .trash {
        cursor: pointer;
        position: absolute;
        top: 50%;
        right: 10px;
        transform: translateY(-50%);
        font-size: 20px;
      }
    }
  }
}
</style>
