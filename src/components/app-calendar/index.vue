<template lang="pug">
  .app-calendar
    .today-title
      span.mr4 {{month}}月
      span {{year}}年
    .weeks
      .weeks__cell.dib(v-for="(title, index) in weekTitleList" :key="index") {{title}}
    v-touch.days(ref="days"
      @swipeleft="handleChangeNextMonth"
      @swiperight="handleChangeLastMonth")
      .days__cell.dib(v-for="index in getMonthDays(year, month)" :key="index" :style="{marginLeft: index === 1 ? (getWeekInMonth(year, month) - 1) * 48 + 'px' : '0px'}")
        .days__cell__text(:class="{'days__cell__text--active': getActiveDay(index), 'days__cell__text--disabled': getDisabledDay(index)}") {{index}}
</template>

<script>

export default {
  name: 'app-calendar',
  data() {
    return {
      weekTitleList: ['一', '二', '三', '四', '五', '六', '日'],
      today: '',
      year: '',
      month: ''
    }
  },
  mounted() {
    this.setDefaultDate()
  },
  methods: {
    setDefaultDate() {
      const today = new Date()
      this.year = today.getFullYear()
      this.month = today.getMonth() + 1
      this.day = today.getDate()
      this.today = this.year + '-' + (this.month < 10 ? '0' + this.month : this.month) + '-' + (this.day < 10 ? '0' + this.day : this.day)
    },
    getDisabledDay(index) {
      const today = new Date()
      const curYear = today.getFullYear()
      const curMonth = today.getMonth() + 1
      return this.year > curYear || this.year === curYear && (this.month > curMonth || this.month === curMonth && index > this.day)
    },
    getActiveDay(index) {
      const today = new Date()
      const curYear = today.getFullYear()
      const curMonth = today.getMonth() + 1
      return curYear === this.year && curMonth === this.month && this.day === index
    },
    getWeekInMonth(year, month) {
      const weekDay = new Date(year + '/' + month + '/' + '01').getDay()
      return weekDay || 7
    },
    getMonthDays(year, month) {
      return new Date(year, month, 0).getDate()
    },
    handleChangeLastMonth() {
      if (this.month === 1) {
        this.month = 12
        this.year = this.year - 1
      } else {
        this.month = this.month - 1
      }
    },
    handleChangeNextMonth() {
      if (this.month === 12) {
        this.month = 1
        this.year = this.year + 1
      } else {
        this.month = this.month + 1
      }
    }
  }
}
</script>

<style lang="scss" scoped>
$cell-width: 48px;
$cell-heigth: 36px;
.app-calendar {
  background: #f7ebea;
  box-shadow: 0 0 0 1px hsla(0,0%,100%,.3) inset, 0 .5em 1em rgba(0, 0, 0, 0.6);
  width: 350px;
  margin: 20px auto;
  padding-bottom: 8px;
  padding-top: 4px;
  border-radius: 8px;
  overflow: hidden;
  .today-title {
    height: 30px;
    line-height: 30px;
    font-weight: 500;
    margin: 0 auto;
    text-align: center;
  }
  .weeks {
    width: $cell-width * 7;
    &__cell {
      text-align: center;
      line-height: $cell-heigth;
      height: $cell-heigth;
      width: $cell-width;
      font-size: 12px;
    }
  }
  .days {
    width: $cell-width * 7;
    &__cell {
      margin-left: 2px;
      font-size: 12px;
      font-weight: 500;
      text-align: center;
      width: $cell-width;
      height: $cell-heigth;
      &__text {
        margin: 8px auto;
        width: 20px;
        height: 20px;
        line-height: 20px;
        border-radius: 50%;
        &--active {
          background: $color-pl;
        }
        &--disabled {
          color: $color-pl;
        }
      }
    }
  }
}
</style>
