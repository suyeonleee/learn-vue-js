<template>
  <div id="app">
    <button @click="changeMenu('show-list')">목록</button>
    <button @click="changeMenu('input-todo')">추가</button>

    <div class="container">
      <component 
        :is="currentView" 
        @new-todo="insertNewTodo" 
        :showTodo="list"
        @update-todo="updateList"
      ></component>
    </div>

  </div>
</template>

<script>
import InputTodo from './components/InputTodo.vue'
import ShowList from './components/ShowList.vue'

export default {
  name: 'App',
  components: {
    InputTodo,
    ShowList
  },
  data() {
    return {
      currentView: 'ShowList',
      list: [],
      todo: {}
    }
  },
  methods: {
    changeMenu(view) {
      this.currentView = view;
    },
    insertNewTodo(todo) {
      this.list.push(todo);
    },
    updateList(e){
      this.list.todo = e;
      console.log(this.list);
    }
  },
  watch: {
    todo() {
      //console.log(this.todo);
    }
  }
}
</script>

<style>
#app {
  width: 800px;
}
</style>


