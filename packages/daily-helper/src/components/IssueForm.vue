<template>
  <div class="issue-form">
    <h1>daily 快速收集内容帮助表单</h1>
    <el-form>
      <el-form-item label="来源">
        <el-input v-model="params.origin"></el-input>
      </el-form-item>
       <el-form-item label="类型">
        <el-input v-model="params.type"></el-input>
      </el-form-item>
       <el-form-item label="一句话推荐">
        <el-input v-model="params.recommend"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary">复制到粘贴板</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data () {
    return {
      title: '',
      params: {
        origin: '',
        type: '',
        recommend: ''
      }
    }
  }
})
</script>

<style scoped>

</style>
