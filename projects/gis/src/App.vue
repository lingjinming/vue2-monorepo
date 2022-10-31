<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />

    <p>this is gis</p>
    <el-button type="warning" @click="sendToMis">点击给mis传参</el-button>

  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  methods: {
    sendToMis() {
      window.parent.postMessage(`向mis发送数据`, "http://localhost:8080");
    },
  },
  mounted() {
    window.addEventListener(
      "message",
      function (event) {
        console.log("mis来信了：", event);
      },
      false
    );
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
