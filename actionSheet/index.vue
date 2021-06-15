<template>
  <div class="actionsheet-wrap">
    <div class="actionsheet-class actionsheet"
         :class="[show ? 'actionsheet-show': '']">
      <div class="header">
        <div class="title">{{title}}</div>
        <div class="close"
             @click="close">
          <image class="close-img"
                 :src="require('@/static/images/common/close.png')"
                 alt="">
        </div>
      </div>
      <slot name="content">
      </slot>
      <div class="actionsheet-btn actionsheet-cancel"
           hover-class="actionsheet-hover"
           :hover-stay-time="150"
           v-if="isCancel"
           @click="handleClickCancel">取消</div>
    </div>
    <div class="actionsheet-mask"
         :class="[show?'mask-show':'']"
         @click="handleClickMask"></div>
  </div>
</template>

<script>
export default {
  name: "Actionsheet",
  props: {
    title: {
      type: String,
      default: '标题'
    },
    //点击遮罩 是否可关闭
    maskClosable: {
      type: Boolean,
      default: true
    },
    //显示操作菜单
    show: {
      type: Boolean,
      default: false
    },
    //是否需要取消按钮
    isCancel: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    close () {
      this.handleClickCancel()
    },
    handleClickMask () {
      if (!this.maskClosable) return;
      this.handleClickCancel();
    },
    handleClickItem (e) {
      if (!this.show) return;
      const dataset = e.currentTarget.dataset;
      this.$emit('click', {
        index: dataset.index
      });
    },
    handleClickCancel () {
      this.$emit('cancel');
    }
  }
}
</script>

<style lang="scss" scoped>
.actionsheet-wrap {
  .actionsheet {
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 9999;
    visibility: hidden;
    transform: translate3d(0, 100%, 0);
    transform-origin: center;
    transition: all 0.3s ease-in-out;
    background: #fff;
    min-height: 100rpx;
    background: #fff;
    .header {
      display: flex;
      padding: 34rpx;
      font-size: 34rpx;
      font-family: Source Han Sans CN;
      font-weight: 500;
      color: #1a1a1a;
      .title {
        flex: 1;
      }
      .close {
        width: 44rpx;
        height: 44rpx;
        .close-img {
          width: 44rpx;
          height: 44rpx;
        }
      }
    }
  }

  .actionsheet-show {
    transform: translate3d(0, 0, 0);
    visibility: visible;
  }

  .tips {
    width: 100%;
    padding: 30rpx 60rpx;
    box-sizing: border-box;
    text-align: center;
    background: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .operate-box {
    padding-bottom: 12rpx;
  }

  .actionsheet-btn {
    width: 100%;
    height: 100rpx;
    background: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    font-size: 36rpx;
    position: relative;
  }

  .btn-last {
    padding-bottom: env(safe-area-inset-bottom);
  }

  .actionsheet-divider::before {
    content: '';
    width: 100%;
    border-top: 1rpx solid #d9d9d9;
    position: absolute;
    top: 0;
    left: 0;
    -webkit-transform: scaleY(0.5);
    transform: scaleY(0.5);
  }

  .actionsheet-cancel {
    color: #1a1a1a;
    padding-bottom: env(safe-area-inset-bottom);
  }

  .actionsheet-hover {
    background: #f7f7f9;
  }

  .actionsheet-mask {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.6);
    z-index: 9996;
    transition: all 0.3s ease-in-out;
    opacity: 0;
    visibility: hidden;
  }

  .mask-show {
    opacity: 1;
    visibility: visible;
  }
}
</style>