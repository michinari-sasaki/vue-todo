<template>
  <div>
    <header>
      <div class="inner">
        <h1>TODO LIST<span>use: Vue-Cli, TypeScript, LocalStorage, Netlify</span></h1>
      </div>
    </header>
    <div class="contents inner">
      <div class="todo_menu">
        <input type="text" placeholder="Put Your ToDo" v-model.trim="todoTitle" />
        <button v-on:click="addTodo">追加</button>
      </div>
      <div class="todo_heading">
        <p>ID</p>
        <p>タイトル</p>
        <p>状態</p>
        <p>削除</p>
      </div>
      <ul class="todo_list">
        <li v-for="(todo, index) in todos" :key="index" v-bind:class="{ done: todo.status }">
          <p class="todo_list__id">{{ index + 1 }}</p>
          <p class="todo_list__title">{{ todo.title }}</p>
          <div class="todo_list__buttons">
            <button v-if="todo.status" class="done" v-on:click="todoDone(index, todo.title, todo.status)">完了</button>
            <button v-else class="status" v-bind:class="{ done: todo.status }" v-on:click="todoDone(index, todo.title, todo.status)">作業中</button>
            <button class="delete" v-on:click="deleteTodo(index)">削除</button>
          </div>
        </li>
      </ul>
    </div>
    <footer>@ {{ copyDate }} MyToDo</footer>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "LayoutContent",
  data: function(): { copyDate: number; todoTitle: string; todos: any[]; checks: boolean } {
    return {
      copyDate: 0,
      todoTitle: "",
      todos: [],
      checks: true,
    };
  },
  props: {
    msg: String,
  },
  methods: {
    addTodo: function() {
      if (this.todoTitle) {
        this.todos.push({
          title: this.todoTitle,
          status: false,
        });
        this.todoTitle = "";
        this.saveTodo();
      }
    },
    deleteTodo: function(index: number) {
      let tmp = JSON.parse(localStorage.getItem("todos")!);
      tmp.splice(index, 1);
      localStorage.setItem("todos", JSON.stringify(tmp));
      this.loadTodo();
    },
    todoDone: function(index: number, title: string, status: boolean) {
      let tmp = JSON.parse(localStorage.getItem("todos")!);
      tmp.splice(index, 1, { title: title, status: !status });
      localStorage.setItem("todos", JSON.stringify(tmp));
      this.loadTodo();
    },
    saveTodo: function() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    loadTodo: function() {
      this.todos = JSON.parse(localStorage.getItem("todos")!);
      if (!this.todos) {
        this.todos = [];
      }
    },
    getYear: function() {
      this.copyDate = new Date().getFullYear();
    },
  },
  mounted: function() {
    this.getYear();
    this.loadTodo();
    //localStorage.removeItem("todos");
  },
});
</script>

<style scoped lang="scss"></style>
