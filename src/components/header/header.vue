<template>
	<div class="header">
		<div class="content-wrapper">
      <div class="avatar">
          <img src="" height="64" width="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{ seller.name }}</span>
        </div>
        <div class="description">
          {{ seller.description }}/{{  seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
            <span class="icon" :class="classMap[seller.supports[0].type]"></span>
            <span class="text">{{ seller.supports[0].description }}</span>
        </div>
      </div>
      <div class="support-count" v-if="seller.supports">
        <span class="count" @click="showDetail">{{ seller.supports.length }}个</span>
        <span class="icon-keyboard_arrow_right"></span>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span><span class="bulletin-text">{{ seller.bulletin }}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
        <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <div class="detail" v-show="detailShow" transition="fade">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <h1 class="name">{{seller.name}}</h1>
            <div class="star-wrapper">
              <star :size="48" :score="seller.score"></star>
            </div>
            <div class="title">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>
            <ul v-if="seller.supports" class="supports">
                <li class="support-item" v-for="item in seller.supports">
                  <span class="icon" :class="classMap[seller.supports[$index].type]"></span>
                  <span class="text">{{ item.description }}</span>
                </li>
            </ul>
            <div class="title">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>
            <div class="bulletin">
              <p class="cotent">
                {{ seller.bulletin }}
              </p>
            </div>
          </div>
        </div>
        <div class="detail-close">
          <i class="icon-close" @click="hideDetail"></i>
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
    data() {
      return {
        detailShow: false
      };
    },
    methods: {
      showDetail() {
        this.detailShow = true;
      },
      hideDetail() {
        this.detailShow = false;
      }
    },
    created() {
      this.classMap = ['decrease', 'discount', 'guarantee', 'invoice', 'special'];
    },
    components: {
      star
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl";

  .header
    color: #fff
    overflow:hidden
    position: relative
    background: rgba(7, 17, 27,.5)
    .content-wrapper
      padding: 24px 12px 18px 24px
      position: relative
      font-size: 0
      .avatar
        display: inline-block
        vertical-align: top
        img
          border-radius: 2px
      .content
        display: inline-block
        font-size: 14px
        margin-left: 16px
        .title
          margin: 2px 0 8px 0
          .brand
            vertical-align: top
            width: 30px
            height: 18px
            //background-image: url('brand@2x.png')
            bg-image("brand")
            background-size: 30px 18px
            background-repeat: no-repeat
            display: inline-block
          .name
            font-weight: bold
            line-height: 18px
            font-size: 16px
            margin-left: 6px
        .description
          font-size: 12px
          line-height: 12px
          margin-bottom: 8px
        .support
          .icon
            position: relative
            top: 2px
            background-repeat: no-repeat
            background-size: 12px 12px
            display: inline-block
            margin-right: 4px
            height: 12px
            width: 12px
            &.decrease
              bg-image('decrease_1')
            &.discount
              bg-image('discount_1')
            &.guarantee
              bg-image('guarantee_1')
            &.invoice
              bg-image('invoice_1')
            &.special
              bg-image('special_1')
          .text
            margin-top: -2px
            line-height: 12px
            font-size: 12px
      .support-count
        text-align:center
        border-radius: 14px
        background-color: rgba(0, 0, 0, 0.2)
        height: 24px
        padding:0 8px
        bottom: 18px
        right: 12px
        position: absolute
        line-height: 24px
        .count
          font-size: 12px
          display: inline-block
          margin-left: 4px
          height: 100%
        .icon-keyboard_arrow_right
          font-size:  14px
          display: inline-block
          position: relative
          top: 2px
    .bulletin-wrapper
      text-overflow: ellipsis
      overflow: hidden
      white-space: nowrap
      background: rgba(7, 17, 27, .4)
      position: relative
      padding: 0 22px 0 12px
      line-height: 28px
      height: 28px
      .bulletin-title
        background-repeat: no-repeat
        background-size: 22px 12px;
        vertical-align: top
        margin-top: 8px
        bg-image('bulletin')
        height: 12px
        display: inline-block
        width: 22px
      .bulletin-text
        margin: 0 4px;
        font-size: 10px
        vertical-align: top
      .icon-keyboard_arrow_right
        position: absolute
        right: 12px
        top: 8px
        font-size: 10px
    .background
      position: absolute
      width: 100%
      height: 100%
      z-index: -1
      top: 0
      left: 0
      filter: blur(10px)
    .detail
      position: fixed
      z-index: 100
      top: 0
      left: 0
      width: 100%
      height: 100%
      overflow-y: auto
      backdrop-filter: blur(10px)
      transition: all .5s
      &.fade-transition
        opacity: 1
        background: rgba(7, 17, 27, .8)
      &.fade-enter,&.fade-leave
        opacity: 0
        background: rgba(7, 17, 27, 0)
      .detail-wrapper
        min-height: 88%
        width: 100%
        .detail-main
          margin-top: 64px
          padding-bottom: 64px
          .name
            line-height: 16px
            text-align: center
            font-size: 16px
            font-weight: 700
          .star-wrapper
            text-align: center
            padding: 2px 0
            margin-top: 18px
          .title
            display: flex
            width: 80%
            margin: 30px auto 24px auto
            .line
              flex: 1
              position: relative
              top: -6px
              border-bottom: 1px solid rgba(255,255,255,.2)
            .text
              padding: 0 12px
              font-size: 14px
              font-weight: 700
          .supports
            width: 80%
            margin: 0 auto
            .support-item
              padding: 0 12px
              margin-bottom: 12px
              font-size: 0
              &:last-child
                margin-bottom: 0
              .icon
                display: inline-block
                width: 16px
                height: 16px
                vertical-align: top
                margin-right: 6px
                background-size: 16px 16px
                background-repeat: no-repeat
                &.decrease
                  bg-image('decrease_2')
                &.discount
                  bg-image('discount_2')
                &.guarantee
                  bg-image('guarantee_2')
                &.invoice
                  bg-image('invoice_2')
                &.special
                  bg-image('special_2')
              .text
                line-height: 16px
                height: 12px
                display: inline-block
                font-size: 12px
          .bulletin
            width: 80%
            margin: 0  auto
            .content
              padding: 0 12px
              line-height: 24px
              font-size: 12px
      .detail-close
        position: relative
        width: 32px
        height: 32px
        margin: -64px auto 0 auto
        clear: both
        font-size: 32px
</style>
