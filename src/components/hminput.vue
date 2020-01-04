<template>
   <input type="text" class="hminput"
    @input="handleinput" @blur="handleblur"
    :class="{'success':status ,'error':!status}">
</template>

<script>
export default {
  props: ['rules', 'msg'],
  data () {
    return {
      status: true
    }
  },

  methods: {
    handleinput (e) {
      let value = e.target.value
      if (this.rules && this.rules.test(value)) {
        this.status = true
      } else {
        this.status = false
      }
      this.$emit('input', value)
    },

    handleblur (e) {
      let value = e.target.value
      if (this.rules && !this.rules.test(value)) {
        this.$toast.fail({
          message: (this.msg || '输入不正确'),
          duration: 1000
        })
      }
    }

  }

}
</script>

<style lang='less' scoped>
    .hminput{
        width:318/360*100vw;
        height: 60px;
        outline:none;
        border:none;
        border-bottom: 3px solid #ccc;
        font-size: 20px;
        line-height: 60px;
    }
    .success{
        border-bottom-color:green;
    }
    .error{
        border-bottom-color:red;
    }
</style>
