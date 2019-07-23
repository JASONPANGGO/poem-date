<template>
  <div id="app">
    <Date />
    <Signer />
  </div>
</template>

<script>
import Date from "./components/Date.vue";
import Signer from "./components/Signer";
export default {
  name: "app",
  components: {
    Date,
    Signer
  }
};
</script>

<style>
body {
  margin: 0;
}
#app {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
