<template>
  <div class="test">
    <markdown-docs :code="code" :scope="scope"></markdown-docs>
  </div>
</template>
<script>
import axios from 'axios'
import markdownDocs from '../components/code-run'

import moment from 'moment'
export default {
  data () {
    return {
      code: '',
      scope: {
        moment,
        axios
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