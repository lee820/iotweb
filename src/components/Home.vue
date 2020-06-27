<template>
    <el-container class="main-container">
        <!-- 头部区域 -->
        <el-header>
            <div>
                <!-- <img src="../assets/logo.png" alt=""> -->
                <span>物联网操作系统</span>
            </div>
            <el-button type="info" @click="LogOut">退出</el-button>
        </el-header>
        <!-- 主体区域 -->
        <el-container>
            <!-- 侧边栏 -->
            <el-aside :width="isCollaps ? '64px' : '200px'">
                <div class="hide-aside" @click="toggleAside">|||</div>
                <el-menu background-color="#333744" text-color="#ffffff" active-text-color="#409fff"
                :collapse="isCollaps" :collapse-transition="false" :router="true">
                    <!-- 一级菜单 -->
                    <el-submenu index="1">
                        <!-- 一级菜单的模板 -->
                        <template slot="title">
                        <i class="el-icon-location"></i>
                        <span>导航一</span>
                        </template>
                        <!-- 二级菜单 -->
                        <el-menu-item index="1-2">
                            <i class="el-icon-menu"></i>
                            <span slot="title">选项二</span>
                        </el-menu-item>
                    </el-submenu>
                </el-menu>
            </el-aside>
            <!-- 主题区域 -->
            <el-main>
                <router-view></router-view>
            </el-main>
        </el-container>
    </el-container>
</template>

<script>
export default {
  data () {
    return {
      // 左侧菜单是否折叠
      isCollaps: false
    }
  },
  methods: {
    LogOut () {
      window.sessionStorage.clear()
      this.$router.push('/login')
    },
    /*
     * 点击按钮展开，折叠侧边菜单
     */
    toggleAside () {
      this.isCollaps = !this.isCollaps
    }
  }
}
</script>

<style scoped>
.main-container {
    height: 100%;
}

.el-header {
    background-color: #373d41;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: #ffffff;
    font-size: 20px;
}

.el-aside {
    background-color: #333744;
}

.el-main {
    background-color: #eaedf1;
}

.el-aside .el-menu {
    border-right: 0;
}

.hide-aside {
    background-color: #333744;
    font-size: 10px;
    line-height: 24px;
    color: #ffffff;
    text-align: center;
    letter-spacing: 2px;
    cursor: pointer;
}
</style>
