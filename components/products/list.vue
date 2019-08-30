<template>
  <div class="m-products-list">
    <dl>
      <dd
        :class="[item.name,item.active?'s-nav-active':'']"
        :key="item.name"
        @click="navSelect"
        v-for="item in nav"
      >{{item.txt}}</dd>
    </dl>
    <ul>
      <Item
        :key="idx"
        :meta="item"
        v-for="(item,idx) in list"
      />
    </ul>
  </div>
</template>

<script>
import Item from "./product";
export default {
  props: {
    list: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  data() {
    return {
      nav: [
        { name: "s-default", txt: "智能排序", active: true },
        { name: "s-price", txt: "价格最低", active: false },
        { name: "s-visit", txt: "人气最高", active: false },
        { name: "s-comment", txt: "评价最高", active: false }
      ],
    };
  },
  components: {
    Item
  },
  methods: {
    navSelect() {}
  }
};
</script>

<style lang='css'>
</style>
