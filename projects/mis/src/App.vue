<template>
  <div id="app">
    <div ref="chart" class="chart"></div>
    <div>
      <p>this is mis</p>
      <p>
        <el-button type="sucess" @click="changePoint">点击给gis传参</el-button>
      </p>
    </div>
    <!-- <iframe src="http://localhost:8081/" frameborder="0"></iframe> -->
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      gisFrame: null,
    };
  },
  mounted() {
    document.domain = "localhost";
    this.$nextTick(() => this.getEchartData());
    this.gisFrame = window.open("http://localhost:8081/", "gisFrame");

    window.addEventListener(
      "message",
      function (event) {
        if (event.origin == "http://localhost:8081") {
          console.log("gis来信了：", event);
        }
      },
      false
    );
  },
  methods: {
    changePoint() {
      console.log(this.gisFrame);
      let i = 0;
      i++;
      // window.frames[0].postMessage(
      //   `这是第${i}次从mis向gis发送数据`,
      //   "http://localhost:8081/"
      // ); // 触发跨域子页面的messag事件
      this.gisFrame.postMessage(
        `这是第${i}次从mis向gis发送数据`,
        "http://localhost:8081/"
      );
    },
    getEchartData() {
      const chart = this.$refs.chart;
      if (chart) {
        const myChart = this.$echarts.init(chart);
        const option = {
          // backgroundColor: "#0f375f",
          grid: {
            top: "12%",
            lef: "15%",
            // right: "15%",
            bottom: "20%", //也可设置left和right设置距离来控制图表的大小
          },
          tooltip: {
            trigger: "axis",
            axisPointer: {
              type: "shadow",
              label: {
                show: true,
              },
            },
          },
          xAxis: {
            data: ["1月", "2月", "3月", "4月"],
            axisLine: {
              show: true, //隐藏X轴轴线
              lineStyle: {
                color: "#01FCE3",
              },
            },
            axisTick: {
              show: true, //隐藏X轴刻度
            },
            axisLabel: {
              show: true,
              textStyle: {
                color: "#fff", //X轴文字颜色
              },
            },
          },
          yAxis: [
            {
              type: "value",
              name: "单位：篇",
              nameTextStyle: {
                color: "#fff",
              },
              splitLine: {
                show: false,
              },
              axisTick: {
                show: true,
              },
              axisLine: {
                show: true,
                lineStyle: {
                  color: "#FFFFFF",
                },
              },
              axisLabel: {
                show: true,
                textStyle: {
                  color: "#fff",
                },
              },
            },
            {
              type: "value",
              name: "单位：次",
              nameTextStyle: {
                color: "#fff",
              },
              position: "right",
              splitLine: {
                show: false,
              },
              axisTick: {
                show: false,
              },
              axisLine: {
                show: false,
              },
              axisLabel: {
                show: true,
                // formatter: "{value} %", //右侧Y轴文字显示
                formatter: "{value} ", //右侧Y轴文字显示
                textStyle: {
                  color: "#fff",
                },
              },
            },
            {
              type: "value",
              gridIndex: 0,
              min: 50,
              max: 100,
              splitNumber: 8,
              splitLine: {
                show: false,
              },
              axisLine: {
                show: false,
              },
              axisTick: {
                show: false,
              },
              axisLabel: {
                show: false,
              },
            },
          ],
          series: [
            {
              name: "销售水量",
              type: "line",
              yAxisIndex: 1, //使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用
              smooth: true, //平滑曲线显示
              showAllSymbol: true, //显示所有图形。
              symbol: "circle", //标记的图形为实心圆
              symbolSize: 10, //标记的大小
              itemStyle: {
                //折线拐点标志的样式
                color: "#f59a23",
              },
              lineStyle: {
                color: "#f59a23",
              },
              areaStyle: {
                color: "rgba(5,140,255, 0.2)",
              },
              data: [4.2, 3.8, 4.8, 3.5],
            },
            {
              name: "主营业务",
              type: "bar",
              barWidth: 15,
              itemStyle: {
                normal: {
                  color: {
                    type: "linear",
                    x: 0,
                    y: 0,
                    x2: 1,
                    y2: 0,
                    colorStops: [
                      {
                        offset: 0,
                        color: "#00FFE3", // 0% 处的颜色
                      },
                      {
                        offset: 1,
                        color: "#4693EC", // 100% 处的颜色
                      },
                    ],
                    globalCoord: false, // 缺省为 false
                  },
                },
              },
              data: [4.2, 3.8, 4.8, 3.5, 2.9, 2.8, 3, 5],
            },
          ],
        };
        myChart.setOption(option);
        window.addEventListener("resize", function () {
          myChart.resize();
        });
      }
      this.$on("hook:destroyed", () => {
        window.removeEventListener("resize", function () {
          myChart.resize();
        });
      });
    },
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
.chart {
  width: 100%;
  height: 300px;
}
</style>
