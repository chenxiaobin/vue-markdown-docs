### vue-markdown-docs

#### 安装
```
npm install @lekima/vue-markdown-docs
```

#### 属性


参数  | 说明 | 类型 | 可选值 | 默认值 |
---|---|---|---|---|
code  | vue示例代码，单文件组件          | string |
scope | 单文件组件中，从外部import的组件 | object |


#### 示例

[demo](https://chenxiaobin.github.io/vue-markdown-docs/lib/index.html#/)

##### 需要展示的代码 `code.vue`
```
<template>
  <div>{{msg}}</div>
</template>
<script>
export default {
  data () {
    return {
      msg: '测试'
    }
  },
  mounted () {
    this.msg = moment().format('YYYY-MM-DD HH:mm:ss')
  }
}
</script>
<style></style>
```

##### 示例代码
```
<template>
  <div class="test">
    <markdown-docs :code="code" :scope="scope"></markdown-docs>
  </div>
</template>
<script>
import axios from 'axios'
import markdownDocs from '../components/index'

import moment from 'moment'
export default {
  data () {
    return {
      code: '',
      scope: {
        moment
      }
    }
  },
  components: {
    markdownDocs
  },
  mounted () {
    this.getCode()
  },
  methods: {
    getCode () {
      let url = './code.vue'
      axios.get(url).then((result) => {
        this.code = result.data
      })
    }
  }
}
</script>
<style>
.test{
  width: 100%;
  height: 100%;
}
</style>
```

![](https://raw.githubusercontent.com/chenxiaobin/vue-markdown-docs/master/public/images/test.jpg)
