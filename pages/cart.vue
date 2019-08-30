<template>
  <div class="page-cart">
    <el-row>
      <el-col
        :span="24"
        class="m-cart"
        v-if="cart.length"
      >
        <list :cart-data="cart" />
        <p>
          应付金额：
          <em class="money">￥{{total}}</em>
        </p>
        <div class="post">
          <el-button
            @click="submit"
            type="primary"
          >提交订单</el-button>
        </div>
      </el-col>
      <el-col
        :span="24"
        class="empty"
        v-else
      >购物车为空</el-col>
    </el-row>
  </div>
</template>

<script>
import List from "@/components/cart/list";
export default {
  data() {
    return {
      cart: []
    };
  },
  components: {
    List
  },
  computed: {
    total() {
      let total = 0;
      this.cart.forEach(item => {
        total += item.price * item.count;
      });
      return total;
    }
  },
  methods: {
    submit() {}
  },
  async asyncData(ctx) {
    let {
      status,
      data: {
        code,
        data: { name, price }
      }
    } = await ctx.$axios.post("/cart/getCart", {
      id: ctx.query.id
    });
    if (status === 200 && code === 0) {
      console.log(name, price);
      return {
        cart: [
          {
            name,
            count: 1,
            price
          }
        ],
        cartNo: ctx.query.id
      };
    }
  }
};
</script>

<style lang='scss'>
@import "@/assets/css/cart/index.scss";
</style>
