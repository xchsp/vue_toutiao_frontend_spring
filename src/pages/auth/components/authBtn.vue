<template>
  <div @click="handleClick" class="btn">{{text}}</div>
</template>

<script>
export default {
  props: ['text'],
  methods: {
    handleClick(event) {
      this.$emit('click')
    }
  }
}
</script>

<style lang="less" scoped>
.btn {
  width: 69.444vw;
  height: 13.333vw;
  line-height: 13.333vw;
  color: #fff;
  background-color: #cc3300;
  border-radius: 6.667vw;
  text-align: center;
}
</style>