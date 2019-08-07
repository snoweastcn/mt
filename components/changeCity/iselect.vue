<template>
  <div class="m-iselect">
    <span class="name">按省份选择：</span>
    <el-select
      placeholder="省份"
      v-model="pvalue"
    >
      <el-option
        :key="item.value"
        :label="item.label"
        :value="item.value"
        v-for="item in province"
      />
    </el-select>
    <el-select
      :disabled="!city.length"
      placeholder="城市"
      v-model="cvalue"
    >
      <el-option
        :key="item.value"
        :label="item.label"
        :value="item.value"
        v-for="item in city"
      />
    </el-select>
    <span>直接搜索：</span>
    <el-autocomplete
      :fetch-suggestions="querySearchAsync"
      placeholder="请输入城市中文或拼音"
      v-model="input"
    />
  </div>
</template>

<script>
import _ from "lodash";
export default {
  data() {
    return {
      province: [],
      pvalue: "",
      city: [],
      cvalue: "",
      input: "",
      cities: []
    };
  },
  watch: {
    async pvalue(newPvalue) {
      let {
        status,
        data: { city }
      } = await this.$axios.get(`/geo/province/${newPvalue}`);
      if (status === 200) {
        this.city = city.map(item => {
          return {
            value: item.id,
            label: item.name
          };
        });
        this.cvalue = "";
      }
    }
  },
  async mounted() {
    let {
      status,
      data: { province }
    } = await this.$axios.get("/geo/province");
    if (status === 200) {
      this.province = province.map(item => {
        return {
          value: item.id,
          label: item.name
        };
      });
    }
  },
  methods: {
    querySearchAsync: _.debounce(async function(query, cb) {
      if (this.cities.length) {
        cb(this.cities.filter(item => item.value.indexOf(query) > -1));
      } else {
        let {
          status,
          data: { city }
        } = await this.$axios.get("/geo/city");
        if (status === 200) {
          this.cities = city.map(item => {
            return { value: item.name };
          });
          cb(this.cities.filter(item => item.value.indexOf(query) > -1));
        } else {
          cb([]);
        }
      }
    }, 200),
    handleSelect(item) {
      console.log(item.value);
    }
  }
};
</script>

<style lang='scss'>
@import "@/assets/css/changecity/iselect.scss";
</style>
