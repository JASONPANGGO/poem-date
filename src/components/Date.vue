<template>
  <div class="date">
    <div class="today">{{todayString}}</div>
    <div class="week">
      <div class="week-day" v-for="(day, index) in week" :key="index">{{day}}</div>
    </div>
    <div class="days">
      <div
        class="day"
        v-for="(date, index) in days"
        :key="index"
        :class="{todayDay: date == today.getDate(), signed: signed && date == today.getDate()}"
      >{{date}}</div>
    </div>
  </div>
</template>

<script>
import { EventBus } from "./eventBus";

export default {
  name: "Date",
  data() {
    return {
      today: new Date(),
      week: ["日", "一", "二", "三", "四", "五", "六"],
      signed: false
    };
  },
  mounted() {
    EventBus.$on("sign", today => {
      console.log(today);
      this.signed = true;
    });
  },
  computed: {
    todayString: function() {
      return this.today.toLocaleDateString();
    },
    days: function() {
      let today = this.today;
      let currentDays = new Date(
        today.getFullYear(),
        today.getMonth() + 1,
        0
      ).getDate(); // 当月有多少天
      let firstDay = today.getDay() - (today.getDate() % 7) + 1; // 获取当月第一天是星期几
      console.log(firstDay);
      let days = [];
      for (let i = 1; i <= currentDays; i++) {
        days.push(i);
      }
      for (let i = 0; i < firstDay; i++) {
        days.unshift("");
      }
      return days;
    }
  }
};

new Date().toDateString;
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
// 借鉴了Rem布局
@function pxWithVw($n) {
  @return 100vw * $n / 375;
}
// 规定极限宽度，避免PC上观感太差
@function pxWithVwMax($n) {
  @return 480px * $n / 375;
}
.date {
  width: pxWithVw(350);
  max-width: pxWithVwMax(300);
  height: pxWithVw(400);
  max-height: pxWithVwMax(400);
}
.today,
.week {
  width: 100%;
  height: 3em;
  line-height: 3em;
  text-align: center;
}
.week {
  width: pxWithVw(300);
  max-width: pxWithVwMax(300);
  display: flex;
  justify-content: space-around;
  margin: 0 auto;
  border-top: 1px solid rgb(0, 106, 82);
  border-radius: 10px;
}
.days {
  width: pxWithVw(300);
  max-width: pxWithVwMax(300);
  height: pxWithVw(300);
  max-height: pxWithVwMax(300);
  margin: 0 auto;
  display: flex;
  flex-flow: row wrap;
  align-content: flex-start;
}
.day {
  width: pxWithVw(300) / 7;
  height: pxWithVw(300) / 7;
  text-align: center;
  line-height: pxWithVw(300) / 7;
  align-self: flex-start;

  max-width: pxWithVwMax(300) / 7;
  max-height: pxWithVwMax(300) / 7;
  transition: 0.3s ease-in-out;
}
.todayDay {
  background-color: #eeeeee;
  border-radius: 5px;
}
.signed{
  background-color: rgb(0, 106, 82);
}
</style>
