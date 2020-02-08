<template>
  <div>
    <floor
      :floorItem="floorItem.parent"
      :parentLength="parentLength-1"
      @reply="reply"
      v-if="floorItem.parent"
    ></floor>
    <div class="floorWrapper">
      <div class="meta">
        <div class="info">
          {{parentLength}} {{floorItem.user.nickname}}
          <span class="time">{{parentLength}}小时前</span>
        </div>
        <div @click="reply" class="btnApply">回复</div>
      </div>
      <div class="content">{{floorItem.content}}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['floorItem', 'parentLength'],
  name: 'floor',
  methods: {
    reply(data) {
      // 判断是递归层传递还是自身传递
      if (data.id) {
        this.$emit('reply', data)
      } else {
        this.$emit('reply', {
          // 把评论回复id传到父组件,由于递归自调用此时父组件还是floorComment组件
          id: this.floorItem.id
        })
      }
    }
  }
}
</script>
<style lang="less" scoped>
  .floorWrapper {
    border: 1px solid #eee;
    background-color: #f3f3f3;
    padding: 10/@vv;
  }
  .meta {
    display: flex;
    justify-content: space-between;
    .info {
      font-size: 12px;
      color: #888;
    }
    .btnApply {
      font-size: 12px;
      color: #888;
    }
  }
  .content {
    margin-top: 10/@vv;
  }
</style>
