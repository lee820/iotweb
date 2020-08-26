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
            <!-- 分页数量显示 -->
            <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page.sync="page"
                :page-size="pagesize"
                layout="total, prev, pager, next"
                :total="totalPage">
            </el-pagination>
        </el-card>
    </div>
</template>

<script>
export default {
  data () {
    return {
      deviceTablaData: [],
      page: 1,
      pagesize: 5,
      totalPage: 0
    }
  },
  created () {
    this.GetDeviceList(1, 5)
  },
  methods: {
    /*
    * 获取设备信息列表
    */
    GetDeviceList (page, pagesize) {
      this.$http({
        method: 'get',
        url: '/api/v1/device/1',
        params: {
          page: page,
          pagesize: pagesize
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
        this.totalPage = res.data.pager.total_rows
      }).catch(error => {
        console.log(error)
      })
    },
    /*
     * 分页显示大小改变
     */
    handleSizeChange (val) {
      console.log(`每页 ${val} 条`)
    },

    /*
     * 当前分页改变
     */
    handleCurrentChange (val) {
      console.log(`当前页: ${val}`)
      this.GetDeviceList(val, this.pagesize)
    }
  }
}
</script>

<style scoped>

</style>
