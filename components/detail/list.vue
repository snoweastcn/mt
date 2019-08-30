<template>
  <div class="m-detail-list">
    <ul>
      <li>{{list.filter(item=>item.photos.length).length}}款套餐</li>
      <item
        :key="idx"
        :meta="item"
        v-for="(item,idx) in list"
      />
    </ul>
  </div>
</template>

<script>
import Item from "./item";
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
    return {};
  },
  components: {
    Item
  }
};
</script>

<style lang='css'>
</style>
