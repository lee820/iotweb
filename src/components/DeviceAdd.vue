<template>
    <div class="devAdd">
        <el-form ref="DevFormRef" label-width="80px" :model="DevForm" class="dev_form">
            <el-form-item label="设备名称">
                <el-input v-model="DevFormRef.name"></el-input>
            </el-form-item>
            <el-form-item label="设备地址">
                <el-input v-model="DevFormRef.place"></el-input>
            </el-form-item>
            <el-form-item label="设备类型">
                <el-input v-model="DevFormRef.type"></el-input>
            </el-form-item>
        </el-form>
    </div>
</template>

<script>
export default {
  data () {
    return {
      DevFormRef: {
        name: '',
        place: '',
        type: ''
      }
    }
  }
}
</script>

<style scoped>

</style>
