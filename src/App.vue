<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div class="inp">
      <input type="text" placeholder="input todo" class="todo-content" v-model.lazy="newTodoContent">
      <button type="button" class="add" @click="addTodo">添加</button>
    </div>
    <transition-group name="todo"  class="todo-container">
      <li v-for="item in todos" :key="item.id" class="todo">
        <span>{{item.content}}</span>
        <button @click="finishTodo(item)">完成</button>
      </li>
    </transition-group>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  // name: 'App',
  // components: {
  //   HelloWorld
  // }
  data(){
    return{
      todos: [],
      newTodoContent: "",
    }
  },
  methods:{
    addTodo(){
      if(!this.newTodoContent){
        return;
      }
      this.todos.unshift({
        id:this.randomId(),
        content:this.newTodoContent,
      })
      this.newTodoContent = "";
    },
    finishTodo(item){
      this.todos = this.todos.filter((it) => it !== item);
    },
    randomId() {
      return Math.random()
        .toString(16)
        .substr(2, 5);
    }
  }
}
</script>

<style lang="less" scoped>
#app {
  width: 600px;
  margin: 1em auto;

  padding: 1.5em;
  border-radius: 5px;
  position: relative;
}
.inp{
  margin: 1em 0;
}
.todo-content{
  display: block;
  box-sizing: border-box;
  width: 100%;
  height: 50px;
  outline: none;
  margin: 1em auto;
  font-size: 1.3em;
  padding: 0 1em;
  border-radius: 5px;
  border: 1px solid #ccc;
}
.add{
  width: 100px;
  height: 30px;
}
.todo-container {
  list-style: none;
  padding: 0;
  margin: 1em 0;
}

.todo{
  // display: inline-block;
  width: 100%;
  position: relative;
  list-style: none;
  padding: 1em 0;
  border-bottom: 1px solid #ccc;
   word-break:break-all;
  button{
    position: absolute;
    right: 0;
  }
}
.todo-enter{
  opacity: 0;
  transform: translateX(-100%);
}
.todo-leave-to{
  opacity: 0;
  transform: translateX(100%);
}
.todo-enter-active,.todo-leave-active,.todo-move{
  transition: .5s;
}
.todo-leave-active {
  position: absolute;
}
</style>
