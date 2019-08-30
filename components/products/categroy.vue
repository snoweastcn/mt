<template>
  <div class="m-product-categroy">
    <dl class="classic">
      <dt>分类</dt>
      <dt>全部</dt>
      <dd
        :key="idx"
        v-for="(item,idx) in types"
      >
        <iselect
          :list="item.module"
          :name="item.type"
        />
      </dd>
    </dl>
    <dl class="classic">
      <dt>分类</dt>
      <dt>全部</dt>
      <dd
        :key="idx"
        v-for="(item,idx) in areas"
      >
        <iselect
          :list="item.module"
          :name="item.type"
        />
      </dd>
    </dl>
  </div>
</template>

<script>
import Iselect from "./iselect";
export default {
  props: {
    name: {
      type: String,
      default: ""
    },
    list: {
      type: Array,
      default() {
        return [];
      }
    },
    types: {
      type: Array,
      default() {
        return [];
      }
    },
    areas: {
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
    Iselect
  }
};
</script>

<style lang='css'>
</style>
