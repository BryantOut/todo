<template>
  <div class='real-app'>
    <input
      type="text"
      class='add-input'
      autofocus='autofocus'
      placeholder="接下去要做什么?"
      @keyup.enter='addTodo'
    >
    <Item
      :todo='todo'
      v-for='todo in filteredTodos'
      :key='todo.id'
      @del='deletetodo'
    />
    <!-- @del='deletetodo'接收父子间传递过来的 -->
    <!-- 将整个todos传给子组件 -->
    <Tabs
      :filter='filter'
      :todos='todos'
      @toggle='toggleFilter'
      @clearAllCompleted='clearAllCompleted'
    ></Tabs>
  </div>
</template>

<script>
import Item from './item'
import Tabs from './tabs'
let id = 0
export default {
  data () {
    return {
      todos: [],
      filter: 'all'
    }
  },
  components: {
    Item,
    Tabs
  },
  methods: {
    // 添加记录方法
    addTodo (e) {
      this.todos.unshift({
        id: id++,
        content: e.target.value.trim(),
        completed: false
      })
      // 每次添加记得清空
      e.target.value = ''
    },
    deletetodo (id) {
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1)
    },
    // 当前选中的状态
    toggleFilter (state) {
      this.filter = state
    },
    // 清除完成的
    clearAllCompleted () {
      this.todos = this.todos.filter(todo => !todo.completed)
    }
  },
  computed: {
    // 根据选中状态过滤出要显示的item
    filteredTodos () {
      if (this.filter === 'all') {
        return this.todos
      }
      const completed = this.filter === 'completed'
      return this.todos.filter(todo => completed === todo.completed)
    }
  }
}
</script>

<style lang="stylus" scoped>
.real-app {
  width: 600px;
  margin: 0px auto;
  box-shadow: 0px 0px 5px #666;
}

.add-input {
  positon: relative;
  margin: 0px;
  width: 100%;
  font-size: 24px;
  font-family: inherit;
  font-weight: inherit;
  line-height: 1.4rem;
  border: 0;
  outline: none;
  color: inherit;
  padding: 6px;
  border: 1px solid #999;
  box-shadow: inset 0 -1px 5px 0px rgba(0, 0, 0, 0);
  box-sizing: border-box;
  font-smoothing: antialiased;
  padding: 16px 16px 16px 60px;
  border: none;
}
</style>
