<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <div>
      <p>this is mis</p>
      <p><el-button type="sucess" @click="changePoint">点击给gis传参</el-button></p>
    </div>
    <iframe src="http://localhost:8081" frameborder="0"></iframe>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  methods: {
    changePoint() {
      let i = 0;
      i++;
      window.frames[0].postMessage(
        `这是第${i}次从mis向gis发送数据`,
        "http://localhost:8081"
      ); // 触发跨域子页面的messag事件
    },
  },
  mounted() {
    window.addEventListener(
      "message",
      function (event) {
        console.log("gis来信了：", event);
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
iframe {
  position: absolute;
  width: 90%;
  height: 500px;
  left: 5%;
  right: 5%;
  bottom: 20px;
  border: 1px solid red;
}
</style>
