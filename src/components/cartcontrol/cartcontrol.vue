<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease" @click.stop.prevent="decreaseCart">
        <span class="inner icon-remove_circle_outline"></span>
      </div>
    </transition>
    <div class="cart-count">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click.stop.prevent="addCart($event)"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      food: {
        type: Object
      }
    },
    methods: {
      /*增加食物数量*/
      addCart(event) {
        if (!event._constructed) {
          return
        }
        this.food.count++
      },
      /*减少食物数量*/
      decreaseCart(event) {
        if (!event._constructed) {
          return
        }
        if (this.food.count) {
          this.food.count--
        }
        this.$emit('decrease', event.target)
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">

  .cartcontrol
    font-size 0
    .cart-decrease
      display inline-block
      padding 6px
      opacity 1
      transform translate3d(0, 0, 0)
      .inner
        display inline-block
        line-height 24px
        font-size 24px
        color rgb(0, 160, 220)
        transform rotate(0)
      &.move-enter-active, &.move-leave-active
        transition: all 0.4s linear
        .inner
          transition all 0.4s linear
      &.move-enter, &.move-leave-to
        opacity 0
        transform translate3d(24px, 0, 0)
        .inner
          transform rotate(180deg)
    .cart-count
      display inline-block
      vertical-align top
      width 12px
      padding-top 6px
      line-height 24px
      text-align center
      font-size 10px
      color rgb(147, 153, 159)
    .cart-add
      display inline-block
      padding 6px
      line-height 24px
      font-size 24px
      color rgb(0, 160, 220)
</style>
