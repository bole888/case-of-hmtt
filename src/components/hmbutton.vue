<template>
   <div class="btn" @click="handleclick">
       <span></span>
       <slot></slot>
   </div>
</template>

<script>
export default {
  methods: {
    handleclick (e) {
      this.$emit('click', e)
    }
  }

}
</script>

<style lang='css' scoped>
    .btn{
       width: 318*100vw/360;
       height: 50px;
       background-color: rgb(70, 158, 12);
       border-radius: 25px;
       line-height: 50px;
       text-align: center;
       color:#fff;
       font-weight: bold;
       font-size: 20px;
    }
</style>
