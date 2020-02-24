<template>
  <div class="issue-form">
    <h1>Daily Helper</h1>
    <el-form
      label-position="top"
    >
      <el-form-item label="文章名称">
        <el-input
          v-model="params.title"
          type="textarea"
          autosize
        >
        </el-input>
      </el-form-item>
      <el-form-item
        label="来源"
        placeholder="请选择来源"
      >
        <el-select
          v-model="params.origin"
          class="issue-form__select"
        >
          <el-option
            v-for="(item, index) in origins"
            :key="index"
            :label="item.origin"
            :value="item.origin"
          >
          </el-option>
        </el-select>
      </el-form-item>
      <el-form-item
        label="链接"
      >
        <el-input
          v-model="params.url"
        >
        </el-input>
      </el-form-item>
       <el-form-item
        label="类型"
        placeholder="请选择类型"
       >
        <el-select
          v-model="params.englishName"
          class="issue-form__select"
        >
          <el-option
            v-for="(item, index) in types"
            :key="index"
            :label="item.type"
            :value="item.englishName"
          >
          </el-option>
        </el-select>
      </el-form-item>
       <el-form-item label="一句话推荐">
        <el-input
          v-model="params.recommend"
          type="textarea"
          autosize
        >
        </el-input>
      </el-form-item>
      <el-form-item>
        <el-button
          type="primary"
          class="issue-form__button"
          @click="handleOnCopyCommentToClipboardClick"
        >
          复制内容到粘贴板
        </el-button>
      </el-form-item>
       <el-form-item>
        <el-button
          type="primary"
          class="issue-form__button"
          @click="handleOnCopyTitleToClipboardClick"
        >
          复制标题到粘贴板
        </el-button>
      </el-form-item>
    </el-form>
    <!-- 预览 -->
    <div v-html="html"></div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import marked from 'marked'
import copy from 'copy-to-clipboard'
interface Params {
  title: string;
  origin: string;
  url: string;
  englishName: string;
  recommend: string;
}

interface Type {
  type: string;
  englishName: string;
}

export default Vue.extend({
  data () {
    return {
      origins: [{
        origin: '掘金'
      }, {
        origin: '语雀'
      }, {
        origin: 'Github'
      }, {
        origin: '微信公众号'
      }],
      types: [{
        type: '文章',
        englishName: 'Article'
      }, {
        type: '开源项目',
        englishName: 'OpenSourceProject'
      }, {
        type: '技术团队',
        englishName: 'TechnicalTeam'
      }],
      params: {
        title: '',
        origin: '掘金',
        url: '',
        type: '',
        englishName: 'Article',
        recommend: ''
      },
      html: '',
      title: ''
    }
  },
  methods: {
    handleOnCopyCommentToClipboardClick () {
      const item: Type = this.getType(this.types, this.params.englishName)[0]
      const { markdown, html } = this.generate(this.params, item.type)
      this.html = html
      copy(markdown)
    },
    handleOnCopyTitleToClipboardClick () {
      const item: Type = this.getType(this.types, this.params.englishName)[0]
      this.title = this.generateTitle(item.englishName, this.params.title)
      copy(this.title)
    },
    getType (types: Array<Type>, englishName: string) {
      return types.filter(item => item.englishName === englishName)
    },
    generateTitle (englishName: string, title: string) {
      return `[New ${englishName}] ${title}`
    },
    generate (params: Params, type: string) {
      const markdown = `
1. 来源：[${params.origin}](${params.url})
2. 类型：${type}
3. 推荐语：${params.recommend}
      `
      return {
        markdown,
        html: marked(markdown)
      }
    }
  }
})
</script>

<style lang="scss" scoped>
.issue-form__select, .issue-form__button {
  width: 100%;
}
h1 {
  text-align: center;
}
</style>
