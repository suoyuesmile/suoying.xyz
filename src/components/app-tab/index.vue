<template lang="pug">
  van-tab(
    v-bind="$attrs"
    v-on="$listeners"
    )
    slot
</template>

<script>
import { Tab } from 'vant'
import Vue from 'vue'
import { getColor } from '@/utils'
Vue.use(Tab)

export default {
  name: 'app-tab',
  props: {
    theme: {
      type: String,
      default: 'red'
    }
  },
  computed: {
    getCheckColor() {
      return getColor(this.theme)
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
