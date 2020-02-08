<template>
  <div>
    <div class="commentWraper">
      <div class="meta">
        <img alt class="avatar" src="/static/imgs/default.png" />
        <div class="info">
          <div class="name" v-if="commentItem.user_nickname">{{commentItem.user_nickname}}</div>
          <span class="time">{{commentItem.comment_time|dataFormat}}</span>
        </div>
        <!--<div @click="reply" class="btnApply">回复</div>-->
      </div>
      <!-- 楼层回复 -->
      <!--<floor-->
        <!--:floorItem="commentItem.parent"-->
        <!--:parentLength="parentLength"-->
        <!--@reply="reply"-->
        <!--v-if="commentItem.parent"-->
      <!--/>-->
      <div class="content">{{commentItem.comment_content}}</div>
    </div>
  </div>
</template>

<script>
// import floor from '@/components/floorComment'
export default {
  props: ['commentItem'],
  // components: {
  //   floor
  // },
  data() {
    return {
      // parentLength: this.countParent(0, this.commentItem)
      // parentLength:3
    }
  },
  filters: {
    dataFormat: (data, spe) => {
      data = new Date(data)
      spe = spe || '/'
      var nn = data.getFullYear()
      var mm = data.getMonth() + 1
      var dd = data.getDate()
      return nn + spe + mm + spe + dd
    }
  },
  methods: {
    // countParent(num, obj) {
    //   if (obj.parent) {
    //     return this.countParent(num + 1, obj.parent)
    //   } else {
    //     return num
    //   }
    // },
    // reply(data) {
    //   // 判断是递归层传递还是自身传递
    //   if (data.id) {
    //     this.$emit('reply', data)
    //   } else {
    //     this.$emit('reply', {
    //       // 把评论回复id传到父组件
    //       id: this.commentItem.id
    //     })
    //   }
    // }
  }
}
</script>
<style lang="less" scoped>
  .commentWraper {
    padding: 10/@vv;
    border-bottom: 1px solid #eee;
    .meta {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      margin-bottom: 10px;
      .avatar {
        width: 35/@vv;
        height: 35/@vv;
        border-radius: 50%;
        object-fit: cover;
      }
      .info {
        flex: 1;
        padding-left: 10/@vv;
        .time {
          font-size: 14px;
          color: #888;
        }
      }
      /*.btnApply {*/
      /*font-size: 14px;*/
      /*color: #888;*/
      /*}*/
      .avatar {
        width: 50/@vv;
        height: 50/@vv;
        border-radius: 50%;
        object-fit: cover;
      }
    }
    .content {
      margin-top: 20/@vv;
    }
  }
</style>
