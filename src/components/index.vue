<template>
  <div class="vue-markdown-docs">
    <div class="markdown-config">
      <div class="markdown-config-run" @click="handleCodeChange">运行</div>
      <div class="markdown-config-code">
        <codemirror ref="myCm2"
                v-model="markCode"
                :options="cmOptions">
        </codemirror>
      </div>
    </div>
    <div class="markdown-demo">
      <markdown-run v-if="isLoad" :scope="markScope" :mark="markCode" highlight-style-file-name="github"/>
    </div>
  </div>
</template>
<script>
import Vue from 'vue'
import { codemirror } from 'vue-codemirror'
import 'codemirror/lib/codemirror.css'
import 'codemirror/mode/vue/vue'
import 'codemirror/theme/lesser-dark.css'
import MarkdownRun from 'vue-markdown-run'

Vue.use(MarkdownRun)

export default {
  name: 'markdownDocs',
  props: {
    code: String,
    scope: Object
  },
  components: { codemirror },
  data () {
    return {
      isLoad: true,
      cmOptions: {
        tabSize: 2,
        lineWrapping: true,
        mode: 'text/x-vue',
        theme: 'lesser-dark',
        lineNumbers: true,
        line: true
      },
      type: 'default',
      markCode: '',
      markScope: {}
    }
  },
  watch: {
    code () {
      this.markCode = this.buildCode()
    },
    scope () {
      this.markScope = this.scope
    },
    markCode () {
      this.handleCodeChange()
    }
  },
  mounted () {
    this.markCode = this.buildCode()
    this.markScope = this.scope
  },
  methods: {
    buildCode () {
      return '````html vue-run \n' + this.code + '\n ````'
    },
    handleCodeChange () {
      this.isLoad = false
      this.$nextTick(() => {
        this.isLoad = true
      })
    }
  }
}
</script>
<style>
.vue-markdown-docs{
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.markdown-config{
  width: calc(50% - 2px);
  height: 100%;
  float: left;
  border-right: 1px solid #ddd;
  border-left: 1px solid #ddd;
}
.markdown-config .vue-codemirror,
.markdown-config .CodeMirror{
  height: 100%;
  z-index: 0;
}
.markdown-config .markdown-config-code{
  height: calc(100% - 25px);
}

.markdown-config .markdown-config-run{
  height: 25px;
  line-height: 25px;
  text-align: right;
  cursor: pointer;
  text-decoration: underline;
  color: white;
  font-size: 13px;
  padding-right: 10px;
  background: #262626;
}
.markdown-demo{
  width: 50%;
  height: 100%;
  float: left;
}

.markdown-demo>div{
  width: 100%;
  height: 100%;
}
.markdown-demo .markdown-common{
  display: none;
}
.markdown-demo .vue-markdown-run{
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}
</style>
