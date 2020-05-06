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
