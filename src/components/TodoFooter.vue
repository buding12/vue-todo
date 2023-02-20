<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong>{{ count }}</strong></span
    >
    <ul class="filters" @click="fn">
      <li>
        <a
          :class="{ selected: isSel === 'all' }"
          href="javascript:;"
          @click="isSel = 'all'"
          >全部</a
        >
      </li>
      <li>
        <a
          :class="{ selected: isSel === 'no' }"
          href="javascript:;"
          @click="isSel = 'no'"
          >未完成</a
        >
      </li>
      <li>
        <a
          :class="{ selected: isSel === 'yes' }"
          href="javascript:;"
          @click="isSel = 'yes'"
          >已完成</a
        >
      </li>
    </ul>
    <!-- 8.1绑定点击事件 -->
    <button class="clear-completed" @click="clearFn">清除已完成</button>
  </footer>
</template>

<script>
export default {
  // 7.变量isSell
  data() {
    return {
      isSel: "all", //all是全部完成 ，yes是已完成，no是未完成
    };
  },
  methods: {
    fn() {
      // 在fn中直接获取isSel，传递给父组件
      this.$emit("changeType", this.isSel);
    },
    // 8.2清空已完成-子传父
    clearFn() {
      this.$emit("clear");
    },
  },
  // 6.1定义props
  props: ["farr"],
  // 6.2计算属性
  computed: {
    count() {
      return this.farr.length;
    },
  },
};
</script>