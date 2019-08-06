<template>
  <div class="search-panel">
    <el-row class="m-header-searchbar">
      <el-col
        :span="3"
        class="left"
      >
        <img
          alt="美团"
          src="//s0.meituan.net/bs/fe-web-meituan/e5eeaef/img/logo.png"
        />
      </el-col>
      <el-col
        :span="15"
        class="center"
      >
        <div class="wrapper">
          <el-input
            @blur="blur"
            @focus="focus"
            @input="input"
            placeholder="搜索商家或地点"
            v-model="search"
          ></el-input>
          <button class="el-button el-button--primary">
            <i class="el-icon-search" />
          </button>
          <dl
            class="hotPlace"
            v-if="isHotPlace"
          >
            <dt>热门搜索</dt>
            <dd
              :key="index"
              v-for="(item, index) in $store.state.home.hotPlace.slice(0,5)"
            >{{item.name}}</dd>
          </dl>
          <dl
            class="searchList"
            v-if="isSearchList"
          >
            <dd
              :key="index"
              v-for="(item, index) in searchList"
            >{{item.name}}</dd>
          </dl>
        </div>
        <p class="suggest">
          <a
            :key="index"
            href="#"
            v-for="(item, index) in $store.state.home.hotPlace.slice(0,5)"
          >{{item.name}}</a>
        </p>
        <ul class="nav">
          <li>
            <nuxt-link
              class="takeout"
              to="/"
            >美团外卖</nuxt-link>
          </li>
          <li>
            <nuxt-link
              class="movie"
              to="/"
            >猫眼电影</nuxt-link>
          </li>
          <li>
            <nuxt-link
              class="hotel"
              to="/"
            >美团酒店</nuxt-link>
          </li>
          <li>
            <nuxt-link
              class="apartment"
              to="/"
            >民宿/公寓</nuxt-link>
          </li>
          <li>
            <nuxt-link
              class="business"
              to="/"
            >商家入驻</nuxt-link>
          </li>
        </ul>
      </el-col>
      <el-col
        :span="6"
        class="right"
      >
        <ul class="security">
          <li>
            <i class="refund" />
            <p class="txt">随时退</p>
          </li>
          <li>
            <i class="single" />
            <p class="txt">不满意免单</p>
          </li>
          <li>
            <i class="overdue" />
            <p class="txt">过期退</p>
          </li>
        </ul>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  data() {
    return {
      search: "",
      isFocus: false,
      hotPlace: [],
      searchList: []
    };
  },

  components: {},
  computed: {
    isHotPlace() {
      return this.isFocus && !this.search;
    },
    isSearchList() {
      return this.isFocus && this.search;
    }
  },
  methods: {
    focus() {
      this.isFocus = true;
    },
    blur() {
      setTimeout(() => {
        this.isFocus = false;
      }, 200);
    },
    input: _.debounce(async function() {
      let city = this.$store.state.geo.position.city.replace("市", "");
      this.searchList = [];
      let {
        status,
        data: { top }
      } = await this.$axios.get("/search/top", {
        params: {
          input: this.search,
          city
        }
      });
      this.searchList = top.slice(0, 10);
    }, 300)
  }
};
</script>

<style lang='scss'>
</style>
