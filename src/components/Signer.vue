<template>
  <div class="sign">
    <button v-if="!signed" @click="sign">打卡</button>
    <div class="signed" v-if="signed">今天已打卡</div>
  </div>
</template>

<script>
import { EventBus } from "./eventBus";
export default {
  name: "Signer",
  data() {
    return {
      signed: false
    };
  },
  methods: {
    sign() {
      this.signed = true;
      EventBus.$emit("sign", {
        today: new Date()
      });
    }
  }
};
</script>

<style lang="scss" scoped>
// 借鉴了Rem布局
@function pxWithVw($n) {
  @return 100vw * $n / 375;
}
// 规定极限宽度，避免PC上观感太差
@function pxWithVwMax($n) {
  @return 480px * $n / 375;
}
button,
.signed {
  width: pxWithVw(100);
  max-width: pxWithVwMax(100);
  height: pxWithVw(100);
  max-height: pxWithVwMax(100);
  border-radius: 50%;
  background: radial-gradient(rgb(0, 106, 83), rgb(0, 80, 80));
  border: none;
  font-family: "宋体";
  font-size: 24px;
  color: white;
  outline: none;
}

.signed {
  text-align: center;
  line-height: pxWithVw(100);
  font-size: 18px;
}
</style>