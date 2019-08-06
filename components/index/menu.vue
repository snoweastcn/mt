<template>
  <div class="m-menu">
    <dl
      @mouseleave="mouseleave"
      class="nav"
    >
      <dt>全部分类</dt>
      <dd
        :key="index"
        @mouseenter="mouseenter(index)"
        ref="menuItem"
        v-for="(item,index) in $store.state.home.menu"
      >
        <i :class="item.type" />
        {{item.name}}
        <span class="arrow" />
      </dd>
    </dl>
    <div
      @mouseenter="sover"
      @mouseleave="sout"
      class="detail"
      v-if="kind"
    >
      <template v-for="(item,index) in curdetail.child">
        <h4 :key="index">{{item.title}}</h4>
        <span
          :key="v"
          v-for="v in item.child"
        >{{v}}</span>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      kind: "",
      menu: [
        {
          type: "food",
          name: "美食",
          child: [
            {
              title: "美食",
              child: [
                "代金券",
                "甜点饮品",
                "火锅自助餐",
                "小吃快餐",
                "日韩料理",
                "西餐",
                "聚餐宴请",
                "烧烤烤肉",
                "东北菜",
                "川湘菜",
                "江浙菜",
                "香锅烤鱼",
                "粤港菜",
                "中式烧烤/烤串",
                "西北菜",
                "咖啡酒吧茶馆",
                "云贵菜",
                "东南亚菜",
                "海鲜",
                "素食",
                "台湾/客家菜",
                "创意菜汤/粥/炖菜",
                "蒙餐",
                "新疆菜",
                "其他美食",
                "京菜鲁菜"
              ]
            }
          ]
        },
        {
          type: "takeout",
          name: "外卖",
          child: [
            {
              title: "外卖",
              child: ["美团外卖"]
            }
          ]
        },
        {
          type: "hotel",
          name: "酒店",
          child: [
            {
              title: "酒店",
              child: ["经济型", "舒适/三星", "高档/四星", "豪华/五星"]
            }
          ]
        }
      ]
    };
  },
  components: {},
  computed: {
    curdetail() {
      return this.$store.state.home.menu.filter(item => item.type === this.kind)[0];
    }
  },
  methods: {
    mouseleave() {
      this.tiemer = setTimeout(() => {
        this.kind = "";
      }, 150);
    },
    mouseenter(e) {
      this.kind = this.$store.state.home.menu[e].type;
    },
    sover() {
      clearTimeout(this.tiemer);
    },
    sout() {
      this.kind = "";
    }
  }
};
</script>

