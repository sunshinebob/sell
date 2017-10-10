<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">{{seller.description}} / {{seller.deliveryTime}}分钟送达</div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count" @click="showDetail">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <div v-show="detailShow" class="detail">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
        </div>
      </div>
      <div @click="hideDetail" class="detail-close">
        <i class="icon-close"></i>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import star from 'components/star/star';

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data () {
      return {
        detailShow: false
      };
    },
    methods: {
      showDetail () {
        this.detailShow = true;
      },
      hideDetail () {
        this.detailShow = false;
      }
    },
    created () {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
    components: {
      'v-star': star
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">

  @import "../../common/stylus/mixin.styl"

  .header
    position: relative
    overflow: hidden
    color: #fff
    background-color: rgba(7, 17, 27, 0.5)
    .content-wrapper
      position: relative
      padding: 24px 12px 18px 24px
      font-size: 0
      .avatar
        display: inline-block
        vertical-align: top
        img
          border-radius: 2px
      .content
        display: inline-block
        margin-left: 16px
        font-size: 14px
        vertical-align: top
        .title
          margin: 2px 0 8px 0
          .brand
            display: inline-block
            width: 30px
            height: 18px
            bg-img('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
            vertical-align: top
          .name
            display: inline-block
            font-size: 16px
            line-height: 18px
            vertical-align: top
            margin-left: 6px
        .description
          font-size: 12px
          line-height: 12px
        .support
          margin: 10px 0px 2px 0
          .icon
            display: inline-block
            vertical-align: top
            width: 12px
            height: 12px
            background-size: 12px 12px
            background-repeat: no-repeat
            &.decrease
              bg-img('decrease_1')
            &.discount
              bg-img('discount_1')
            &.guarantee
              bg-img('guarantee_1')
            &.invoice
              bg-img('invoice_1')
            &.special
              bg-img('special_1')
          .text
            display: inline-block
            vertical-align: middle
            margin-left: 4px
            line-height: 12px
            font-size: 10px

      .support-count
        position: absolute
        right: 12px
        bottom: 14px
        padding: 0 8px
        height: 24px
        line-height: 24px
        border-radius: 14px
        background-color: rgba(0, 0, 0, 0.2);
        text-align: center
        .count
          vertical-align: top
          margin-right: 2px
          font-size: 10px
        .icon-keyboard_arrow_right
          line-height: 24px
          font-size: 10px
    .bulletin-wrapper
      position: relative
      height: 28px
      padding: 0 22px 0 12px
      overflow: hidden
      text-overflow: ellipsis
      white-space: nowrap
      background: rgba(7, 17, 27, 0.2)
      .bulletin-title
        display: inline-block
        vertical-align: top
        width: 22px
        height: 12px
        margin-top: 8px
        bg-img('bulletin')
        background-size: 22px 12px
        background-repeat: no-repeat
      .bulletin-text
        position: relative
        top: 1px
        margin-left: 4px
        line-height: 28px
        font-size: 10px
      .icon-keyboard_arrow_right
        position: absolute
        right: 12px
        top: 9px
        font-size: 10px
    .background
      position: absolute
      width: 100%
      height: 100%
      left: 0
      top: 0
      z-index: -1
      filter: blur(10px)
    .detail
      position: fixed
      z-index: 100
      left: 0
      top: 0
      width: 100%
      height: 100%
      overflow: auto
      background: rgba(7, 17, 27, 0.8)
      .detail-wrapper
        min-height: 100%
        .detail-main
          margin-top: 64px
          padding-bottom: 64px
      .detail-close
        position: relative
        width: 32px
        height: 32px
        margin: -64px auto 0 auto
        clear: both
        color:rgba(255,255,255,0.5)
        font-size: 32px
</style>
