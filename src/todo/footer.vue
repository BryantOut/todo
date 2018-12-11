<template>
  <div class='footer'>
    <span>written by {{author}}</span>
  </div>
</template>

<script>
export default {
  data () {
    return {
      author: 'Bryantout@163.com'
    }
  }
}
</script>

<style lang="stylus" scoped>
.footer{
    margin-top 40px
    text-align center
    color #bfbfbf
    font-size 24px
    text-shadow 0px 1px 0px 1px
}
</style>
