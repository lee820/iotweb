<template>
    <div>
        <!-- 面包屑导航 -->
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>概览</el-breadcrumb-item>
        </el-breadcrumb>

        <!-- 卡片视图区域 -->
        <el-card>
            <el-row :gutter="20">
                <el-col :span="8">
                    <el-input placeholder="请输入设备名称">
                        <el-button slot="append" icon="el-icon-search"></el-button>
                    </el-input>
                </el-col>
                <el-col :span="4">
                    <el-button type="primary" @click="GetDeviceList">添加设备</el-button>
                </el-col>
            </el-row>
            <!-- 设备展示表格 -->
            <el-table
                :data="deviceTablaData"
                style="width: 100%">
                <el-table-column
                    prop="name"
                    label="设备名称"
                    width="180">
                </el-table-column>
                <el-table-column
                    prop="place"
                    label="位置"
                    width="180">
                </el-table-column>
                <el-table-column
                    prop="running"
                    label="运行状态">
                </el-table-column>
                </el-table>
        </el-card>
    </div>
</template>

<script>
export default {
  data () {
    return {
      deviceTablaData: [],
      page: 1,
      pagesize: 5
    }
  },
  created () {
    this.GetDeviceList()
  },
  methods: {
    GetDeviceList () {
      this.$http({
        method: 'get',
        url: '/api/v1/device/1',
        params: {
          page: this.page,
          pagesize: this.pagesize
        },
        headers: {
          'Content-Type': 'multipart/form-data'
        }
      }).then((res) => {
        // 1. 将登录成功后的token，保存到客户端的sessionStorage中
        // console.log(res)
        this.deviceTablaData = []
        for (var i = 0; i < res.data.list.length; i++) {
          this.deviceTablaData.push({
            name: res.data.list[i].name,
            place: res.data.list[i].place,
            running: res.data.list[i].running
          })
        }
      }).catch(error => {
        console.log(error)
      })
    }
  }
}
</script>

<style scoped>

</style>
