<template lang="pug">
  van-swipe.swipe(
    :autoplay="2000"
    indicator-color="white"
  )
    van-swipe-item.swipe__item
      img.swipe__item__img(
        :src="require('@/assets/images/index/1.png')"
      )
    van-swipe-item.swipe__item
      img.swipe__item__img(
        :src="require('@/assets/images/index/2.png')"
      )
    van-swipe-item.swipe__item
      img.swipe__item__img(
        :src="require('@/assets/images/index/1.png')"
      )
    van-swipe-item.swipe__item
      img.swipe__item__img(
        :src="require('@/assets/images/index/2.png')"
      )
    van-swipe-item.swipe__item
      img.swipe__item__img(
        :src="require('@/assets/images/index/1.png')"
      )
</template>

<script>
import Vue from 'vue'
import { Swipe, SwipeItem } from 'vant'
Vue.use(Swipe).use(SwipeItem)
export default {

}
</script>

<style lang="scss" scoped>
$height: 225px;
.swipe {
  height: $height;
  &__item {
    text-align: center;
    line-height: $height;
    background: $color-blue;
    color: #fff;
    &__img {
      width: 375px;
      height: $height;
      background-size: $height 375px;
    }
  }
}
</style>
