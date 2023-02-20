<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll" />
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      @keydown.enter="downFn"
      v-model="task"
    />
    <!-- 4.1绑定一个键盘事件,v-model获取name -->
  </header>
</template>

<script>
export default {
  data() {
    return {
      task: "",
    };
  },
  methods: {
    downFn() {
      //  4.3子传父   $emit('自定义事件'，参数)
      this.$emit("create", this.task);
      //  4.6清空表单
      this.task = "";
    },
  },
  // 10.定义计算属性
  computed: {
    isAll: {
      set(checked){ // 只有true / false
                    // 10.3 影响数组里每个小选框绑定的isDone属性
                    this.arr.forEach(obj => obj.isDone = checked)
                },
      get() {
        return (
           // 10.4 小选框统计状态 -> 全选框
                    // 10.5 如果没有数据, 直接返回false-不要让全选勾选状态
          this.arr.length && this.arr.every((obj) => obj.isDone === true)
        );
      },
    },
  },
  //父传给子
    props:['arr']
};
</script>