<template>
  <div id="app">
    <div
      id="echarts"
      ref="echarts"></div>
    <div>
      <button @click="change">改变</button>
    </div>
  </div>
</template>

<script>
import * as echarts from "echarts";
export default {
  name: "App",
  components: {},
  data() {
    return {
      echartsInstance: null,
      options: {
        // 图例
        legend: {
          // 是否显示图例
          show: true,
          textStyle: {
            color: "#000",
            fontSize: 12,
          },
          top: "top",
          left: "right",
          orient: "horizontal",
        },
        // 标题
        title: {
          show: false,
          text: "",
          x: "center",
          textStyle: {
            color: "#000",
            fontStyle: "normal",
            fontWeight: "bold",
            fontSize: "12",
            fontFamily: "normal",
          },
        },
        // 鼠标跟随指示框
        tooltip: {
          show: true,
          trigger: "axis",
        },
        // x轴
        xAxis: {
          // 类别
          type: "category",
          // 是否显示坐标轴
          show: true,
          // 是否反转坐标轴
          inverse: false,
          // 坐标轴留白
          // boundaryGap: "20%",
          // 轴名称
          name: "",
          // 坐标轴名称样式
          nameTextStyle: {
            color: "#000",
            fontSize: 12,
            fontWeight: "normal",
            fontStyle: "normal",
            fontFamily: "normal",
          },
          data: ["a", " b", " c", "d"],
          // x轴文本样式
          axisLabel: {
            // x轴文字的配置
            show: true,
            interval: 0, // 使x轴文字显示全
            color: "#000",
            fontFamily: "normal",
            fontSize: 12,
            fontWeight: "normal",
            fontStyle: "normal",
            formatter: function (params) {
              let newParamsName = "";
              let paramsNameNumber = params.length;
              let provideNumber = 2; // 一行显示几个字
              let rowNumber = Math.ceil(paramsNameNumber / provideNumber);
              if (paramsNameNumber > provideNumber) {
                for (let p = 0; p < rowNumber; p++) {
                  let tempStr = "";
                  let start = p * provideNumber;
                  let end = start + provideNumber;
                  if (p == rowNumber - 1) {
                    tempStr = params.substring(start, paramsNameNumber);
                  } else {
                    tempStr = params.substring(start, end) + "\n";
                  }
                  newParamsName += tempStr;
                }
              } else {
                newParamsName = params;
              }
              return newParamsName;
            },
          },
        },
        // y轴
        yAxis: {
          // 是否显示坐标轴
          show: true,
          // 是否反转坐标轴
          inverse: false,
          // 坐标轴留白
          boundaryGap: ["0", "10%"],
          // 轴名称
          name: "",
          // 坐标轴名称样式
          nameTextStyle: {
            color: "#000",
            fontSize: 12,
            fontWeight: "normal",
            fontStyle: "normal",
            fontFamily: "normal",
          },
          // 轴线样式
          axisLine: {
            show: true,
            lineStyle: {
              color: "#000",
            },
          },
          // y轴文本样式
          axisLabel: {
            // y轴文字的配置
            show: true,
            interval: 0, // 使x轴文字显示全
            color: "#000",
            fontFamily: "normal",
            fontSize: 12,
            fontWeight: "normal",
            fontStyle: "normal",
            formatter: function (params) {
              let newParamsName = "";
              let paramsNameNumber = params.length;
              let provideNumber = 2; // 一行显示几个字
              let rowNumber = Math.ceil(paramsNameNumber / provideNumber);
              if (paramsNameNumber > provideNumber) {
                for (let p = 0; p < rowNumber; p++) {
                  let tempStr = "";
                  let start = p * provideNumber;
                  let end = start + provideNumber;
                  if (p == rowNumber - 1) {
                    tempStr = params.substring(start, paramsNameNumber);
                  } else {
                    tempStr = params.substring(start, end) + "\n";
                  }
                  newParamsName += tempStr;
                }
              } else {
                newParamsName = params;
              }
              return newParamsName;
            },
          },
        },
        // 数据与数据样式
        series: {
          // // 开启动画
          // animation: true,
          // // 设置动画持续时间为 3000 毫秒
          // animationDuration: 3000,
          // // 设置动画缓动效果为圆形进入
          // animationEasing: "circularIn",
          // 数值名称
          name: "abc",
          // 图表类型
          type: "bar",
          // 图表数据
          // data: chosenData[item.value],
          data: [Math.random() * 10, Math.random() * 10, Math.random() * 10],
          // 柱状图宽度
          barWidth: 0,
          // 柱条样式
          itemStyle: {
            // 柱子的颜色
            color: "red",
            // 柱状图圆角
            borderRadius: 0,
          },
          // 是否显示柱的背景颜色
          showBackground: true,
          // 柱的背景颜色设置
          backgroundStyle: {
            color: "rgba(255,255,255,0)",
          },
          // 数值样式
          label: {
            // 是否开启显示数值
            show: true,
            // 在数值显示位置
            position: "top",
            //数值样式
            color: "black",
            // 字体大小
            fontSize: 12,
            // 是否斜体
            fontStyle: "normal",
            // 是否加粗
            fontWeight: "normal",
            // 字体
            fontFamily: "normal",
          },
        },
        // animation: true,
        // animationDuration: 2000,
        // animationEasing: "quinticInOut",
        // animationDelay: 1000,
        // animationDurationUpdate: 2000, // 更新动画时长为 1s
        // animationEasingUpdate: "quinticInOut", // 更新动画缓动效果为 'quinticInOut'
        // animationDelayUpdate: 1000,
      },
    };
  },
  methods: {
    setOptions() {
      const myChart = echarts.init(this.$refs.echarts);
      this.echartsInstance = myChart;
      this.echartsInstance.clear();
      myChart.setOption(this.options);
    },
    change() {
      this.options = {
        // 图例
        legend: {
          // 是否显示图例
          show: true,
          textStyle: {
            color: "#000",
            fontSize: 12,
          },
          top: "top",
          left: "right",
          orient: "horizontal",
        },
        // 标题
        title: {
          show: false,
          text: "",
          x: "center",
          textStyle: {
            color: "#000",
            fontStyle: "normal",
            fontWeight: "bold",
            fontSize: "12",
            fontFamily: "normal",
          },
        },
        // 鼠标跟随指示框
        tooltip: {
          show: true,
          trigger: "axis",
        },
        // x轴
        xAxis: {
          // 类别
          type: "category",
          // 是否显示坐标轴
          show: true,
          // 是否反转坐标轴
          inverse: false,
          // 坐标轴留白
          // boundaryGap: "20%",
          // 轴名称
          name: "",
          // 坐标轴名称样式
          nameTextStyle: {
            color: "#000",
            fontSize: 12,
            fontWeight: "normal",
            fontStyle: "normal",
            fontFamily: "normal",
          },
          data: ["a", " b", " c", "d"],
          // x轴文本样式
          axisLabel: {
            // x轴文字的配置
            show: true,
            interval: 0, // 使x轴文字显示全
            color: "#000",
            fontFamily: "normal",
            fontSize: 12,
            fontWeight: "normal",
            fontStyle: "normal",
            formatter: function (params) {
              let newParamsName = "";
              let paramsNameNumber = params.length;
              let provideNumber = 2; // 一行显示几个字
              let rowNumber = Math.ceil(paramsNameNumber / provideNumber);
              if (paramsNameNumber > provideNumber) {
                for (let p = 0; p < rowNumber; p++) {
                  let tempStr = "";
                  let start = p * provideNumber;
                  let end = start + provideNumber;
                  if (p == rowNumber - 1) {
                    tempStr = params.substring(start, paramsNameNumber);
                  } else {
                    tempStr = params.substring(start, end) + "\n";
                  }
                  newParamsName += tempStr;
                }
              } else {
                newParamsName = params;
              }
              return newParamsName;
            },
          },
        },
        // y轴
        yAxis: {
          // 是否显示坐标轴
          show: true,
          // 是否反转坐标轴
          inverse: false,
          // 坐标轴留白
          boundaryGap: ["0", "10%"],
          // 轴名称
          name: "",
          // 坐标轴名称样式
          nameTextStyle: {
            color: "#000",
            fontSize: 12,
            fontWeight: "normal",
            fontStyle: "normal",
            fontFamily: "normal",
          },
          // 轴线样式
          axisLine: {
            show: true,
            lineStyle: {
              color: "#000",
            },
          },
          // y轴文本样式
          axisLabel: {
            // y轴文字的配置
            show: true,
            interval: 0, // 使x轴文字显示全
            color: "#000",
            fontFamily: "normal",
            fontSize: 12,
            fontWeight: "normal",
            fontStyle: "normal",
            formatter: function (params) {
              let newParamsName = "";
              let paramsNameNumber = params.length;
              let provideNumber = 2; // 一行显示几个字
              let rowNumber = Math.ceil(paramsNameNumber / provideNumber);
              if (paramsNameNumber > provideNumber) {
                for (let p = 0; p < rowNumber; p++) {
                  let tempStr = "";
                  let start = p * provideNumber;
                  let end = start + provideNumber;
                  if (p == rowNumber - 1) {
                    tempStr = params.substring(start, paramsNameNumber);
                  } else {
                    tempStr = params.substring(start, end) + "\n";
                  }
                  newParamsName += tempStr;
                }
              } else {
                newParamsName = params;
              }
              return newParamsName;
            },
          },
        },
        // 数据与数据样式
        series: {
          // // 开启动画
          // animation: true,
          // // 设置动画持续时间为 3000 毫秒
          // animationDuration: 3000,
          // // 设置动画缓动效果为圆形进入
          // animationEasing: "circularIn",
          // 数值名称
          name: "abc",
          // 图表类型
          type: "bar",
          // 图表数据
          // data: chosenData[item.value],
          // data: [Math.random() * 10, Math.random() * 10, Math.random() * 10],
          data: [7, 8, 9, 10],
          // 柱状图宽度
          barWidth: 0,
          // 柱条样式
          itemStyle: {
            // 柱子的颜色
            color: "red",
            // 柱状图圆角
            borderRadius: 0,
          },
          // 是否显示柱的背景颜色
          showBackground: true,
          // 柱的背景颜色设置
          backgroundStyle: {
            color: "rgba(255,255,255,0)",
          },
          // 数值样式
          label: {
            // 是否开启显示数值
            show: true,
            // 在数值显示位置
            position: "top",
            //数值样式
            color: "black",
            // 字体大小
            fontSize: 12,
            // 是否斜体
            fontStyle: "normal",
            // 是否加粗
            fontWeight: "normal",
            // 字体
            fontFamily: "normal",
          },
        },
        animation: true,
        animationDuration: 2000,
        animationEasing: "quinticInOut",
        animationDurationUpdate: 2000, // 更新动画时长为 1s
        animationEasingUpdate: "quinticInOut", // 更新动画缓动效果为 'quinticInOut'
      };
      this.echartsInstance.clear();
      this.echartsInstance.setOption(this.options, true);
    },
  },
  mounted() {
    this.setOptions();
  },
};
</script>

<style lang="scss">

#echarts {
  width: 300px;
  height: 400px;
}
</style>
