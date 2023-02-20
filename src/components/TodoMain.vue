<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <!-- 3.2循环li标签 使用动态css-->
    <li :class="{ completed: obj.isDone }" v-for="obj in arr" :key="obj.id">
      <div class="view">
        <!-- v-model双向数据绑定 -->
        <input class="toggle" type="checkbox" v-model="obj.isDone" />
        <!-- 3.3接收循环的name值 -->
        <label>{{ obj.name }}</label>
        <!-- 5.1绑定事件 -->
        <button class="destroy" @click="delFn(obj.id)"></button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  //3.1 props接收数据
  props: ["arr"],
  methods: {
    delFn(id) {
      // 5.2 子向父传参
      this.$emit("del", id);
    },
  },
};
</script>