<template>
    <el-container class="main-container">
        <!-- 头部区域 -->
        <el-header>
            <div>
                <!-- <img src="../assets/logo.png" alt=""> -->
                <span>物联网操作系统</span>
            </div>
            <!-- 用户信息展示区域 -->
            <div class="user-info">
                <el-avatar icon="el-icon-user-solid"></el-avatar>
                <el-dropdown>
                    <span class="el-dropdown-link">
                        用户lee<i class="el-icon-arrow-down el-icon--right"></i>
                    </span>
                    <el-dropdown-menu slot="dropdown">
                        <el-dropdown-item>用户中心</el-dropdown-item>
                        <el-dropdown-item>待开发</el-dropdown-item>
                    </el-dropdown-menu>
                </el-dropdown>
                <el-button type="info" @click="LogOut">退出</el-button>
            </div>
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
                        <span>首页</span>
                        </template>
                        <!-- 二级菜单 -->
                        <!-- <el-menu-item index="1-2">
                            <i class="el-icon-menu"></i>
                            <span slot="title">选项二</span>
                        </el-menu-item> -->
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
    text-align: right;
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

.el-header .user-info {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 16px;
}

.el-header .user-info .el-avatar {
    margin: 10px;
}

.el-header .user-info > .el-button {
    margin: 10px;
    padding: 10px;
}

.el-dropdown-link {
    cursor: pointer;
    color: #ffffff;
}
</style>
