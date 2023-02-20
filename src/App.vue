<template>
  <!-- 必须有这个类名，否则样式不全面 -->
  <div class="todoapp">
    <!-- 2.2使用组件 -->
    <!-- 4.2绑定自定义事件 -->
    <TodoHeader @create="createFn" :arr='list' ></TodoHeader>
    <!-- 5.3绑定自定义事件 -->
    <TodoMain :arr="showArr" @del="deleteFn"></TodoMain>
    <!-- 6.统计数量：父传子 -->
    <!-- 8.5绑定自定义事件 -->
    <TodoFooter :farr="showArr" @changeType="typeFn" @clear="clearFn"></TodoFooter>
  </div>
</template>

<script>
// 1.先引入css
import "./components/styles/base.css";
import "./components/styles/index.css";
// 2.引入组件
import TodoHeader from "./components/TodoHeader";
import TodoMain from "./components/TodoMain";
import TodoFooter from "./components/TodoFooter";

export default {
  // 3.准备数据
  data() {
    return {
      list: JSON.parse(localStorage.getItem('todoList')) || [],
      
      // 7.0 再定义一个属性，让showArr里面，能够使用 typeFn里面的值（形参）
      getSel: "all",
    };
  },
  methods: {
    // 4.添加任务
    createFn(taskName) {
      // 4.4把数据放入数组
      this.list.push({
        // 4.5判断一下id值是否存在
        id:
          this.list.length === 0 ? 100 : this.list[this.list.length - 1].id + 1,
        name: taskName,
        isDone: false,
      });
    },
    // 5.4删除任务
    deleteFn(theId) {
      let index = this.list.findIndex((obj) => obj.id === theId);
      this.list.splice(index, 1);
    },
    typeFn(str) {
      // 'all' 'yes' 'no' // 修改类型
      this.getSel = str;
    },
    //  8.3清空已完成
    clearFn() {
      this.list = this.list.filter((obj) => obj.isDone === false);
    },
  },

  // 显示的内容是由底部点击按钮计算得到的，因此用计算属性
  computed: {
    showArr() {
      // 不一样的条件下，显示的内容不一致
      if (this.getSel === "yes") {
        // 显示已完成
        return this.list.filter((obj) => obj.isDone === true);
      } else if (this.getSel === "no") {
        // 显示未完成
        return this.list.filter((obj) => obj.isDone === false);
      } else {
        return this.list; // 全部显示
      }
    },
  },
  // 2.1注册组件
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  // 9.数据缓存 --侦听
  watch: {
    list:{
      deep:true,
      handler(){
        localStorage.setItem('todoList',JSON.stringify(this.list))
      }
      
    }
  },
};
</script>

<style>
</style>