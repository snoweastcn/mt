<template>
  <div class="page-index">
    <el-row>
      <el-col :span="5">
        <e-menu />
      </el-col>
      <el-col :span="19">
        <e-life />
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24">
        <e-artistic />
      </el-col>
    </el-row>
  </div>
</template>

<script>
import EMenu from "@/components/index/menu";
import ELife from "@/components/index/life";
import EArtistic from "@/components/index/artistic";
export default {
  components: {
    EMenu,
    ELife,
    EArtistic
  },
  data() {
    return {
      tit: String
    };
  },
  mounted() {
    this.tit = document.title;
    this.titleScrolling();
  },
  methods: {
    titleScrolling() {
      setInterval(() => {
        let head = this.tit.substring(0, 1);
        let foot = this.tit.substring(1);
        this.tit = foot + head;
        document.title = this.tit;
      }, 500);
    }
  }
};
</script>

<style lang="scss">
@import "@/assets/css/index/index.scss";
</style>
