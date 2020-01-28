<template>
  <div>
    <div class="commentWraper">
      <div class="meta">
        <img alt class="avatar" src="/static/imgs/default.png" />
        <div class="info">
          <div class="name" v-if="commentItem.user">{{commentItem.user.nickname}}</div>
          <span class="time">{{commentItem.created}}</span>
        </div>
        <div @click="reply" class="btnApply">回复</div>
      </div>
      <!-- 楼层回复 -->
      <floor
        :floorItem="commentItem.parent"
        :parentLength="parentLength"
        @reply="reply"
        v-if="commentItem.parent"
      />
      <div class="content">{{commentItem.content}}</div>
    </div>
  </div>
</template>

<script>
import floor from '@/components/floorComment'
export default {
  props: ['commentItem'],
  components: {
    floor
  },
  data() {
    return {
      // parentLength: this.countParent(0, this.commentItem)
      parentLength:3
    }
  },
  methods: {
    countParent(num, obj) {
      if (obj.parent) {
        return this.countParent(num + 1, obj.parent)
      } else {
        return num
      }
    },
    reply(data) {
      // 判断是递归层传递还是自身传递
      if (data.id) {
        this.$emit('reply', data)
      } else {
        this.$emit('reply', {
          // 把评论回复id传到父组件
          id: this.commentItem.id
        })
      }
    }
  }
}
</script>
<style lang="less" scoped>
.commentWraper {
  padding: 2.778vw;
  border-bottom: 1px solid #eee;
  .meta {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 10px;
    .avatar {
      width: 9.722vw;
      height: 9.722vw;
      border-radius: 50%;
      object-fit: cover;
    }
    .info {
      flex: 1;
      padding-left: 2.778vw;
      .time {
        font-size: 14px;
        color: #888;
      }
    }
    .btnApply {
      font-size: 14px;
      color: #888;
    }
    .avatar {
      width: 13.889vw;
      height: 13.889vw;
      border-radius: 50%;
      object-fit: cover;
    }
  }
  .content {
    margin-top: 5.556vw;
  }
}
</style>
