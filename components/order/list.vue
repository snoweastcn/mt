<template>
  <div v-if="cur.length">
    <div
      :key="idx"
      v-for="(item,idx) in cur"
    >{{item.name}}</div>
  </div>
  <div v-else>暂无订单数据</div>
</template>

<script>
export default {
  props: {
    cur: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  components: {}
};
</script>

<style lang='css'>
</style>
