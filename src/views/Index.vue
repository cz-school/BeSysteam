<template>
  <div class="app">
    <el-container>
      <el-header class="appHead">
        <h2>五星红旗迎风飘扬🇨🇳🇨🇳</h2>
      </el-header>
      <el-container>
        <el-aside width="200px">
          <el-menu
            background-color="#545c64"
            text-color="#fff"
            active-text-color="#ffd04b"
            :router="true"
            :unique-opened	="true"
          >
            <el-submenu :index="v.name" v-for="(v,i) in userList" :key="i">
              <template slot="title">
                <i class="el-icon-s-unfold"></i>
                {{v.name}}
              </template>
              <el-menu-item :index="v1.router" v-for="(v1,i1) in v.childs" :key="i1">
                <i class="el-icon-s-promotion"></i>
                {{v1.names}}
              </el-menu-item>
            </el-submenu>
          </el-menu>
        </el-aside>
        <el-main>
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>
<script>
export default {
  data() {
    return {
      userList: []
    };
  },
  methods: {
    getUserList() {
      let token = sessionStorage.getItem("_token");
      this.$axios.post("/setUserList",{token}).then(res => {
        console.log(res);
        this.userList = res.data.data;
      });
    }
  },
  created() {
    this.getUserList();
  }
};
</script>
<style>
.el-submenu {
  width: 200px;
  user-select: none;
}
.appHead {
  background: #eee;
  color: rgb(59, 42, 42);
}
.app, .el-container {
  height: 100%;
}
.app .el-aside{
  background: rgb(86, 92, 99);
}
</style>
