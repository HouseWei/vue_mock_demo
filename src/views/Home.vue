<template>
  <div class="container">
    <el-card>
      <el-button type="primary" @click="submitForm('ruleForm')">立即获取</el-button>
    </el-card>
    <el-card>
      <el-table :data="tableData" border stripe style="width:100%">
        <el-table-column
          v-for="(item,index) in tHeaders"
          :key="index"
          :prop="item"
          :label="item"
          align="center"
        ></el-table-column>
      </el-table>
    </el-card>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      ruleForm: {},
      rules: {},
      tableData: []
    }
  },
  computed: {
    tHeaders () {
      if (!this.tableData[0]) return
      var arr = []
      Object.keys(this.tableData[0]).forEach(item => {
        arr.push(item)
      })
      return arr
    }
  },
  created () {},
  methods: {
    submitForm (form) {
      axios
        .get('/user/produce', this.ruleForm)
        .then(res => {
          if (res.status === 200) {
            this.$message.success('获取成功')
          }
          console.log(res)
          this.tableData = res.data.tableData
        })
        .catch(err => {
          console.log(err)
        })
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  .el-card {
    margin-bottom: 15px;
  }
}
</style>
