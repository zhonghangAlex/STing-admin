<template>
  <div ref="dom"></div>
</template>

<script>
import echarts from 'echarts'
import { on, off } from '@/libs/tools'
import tdTheme from '_c/charts/theme.json'
echarts.registerTheme('tdTheme', tdTheme)
export default {
  name: 'robotRate',
  data () {
    return {
      dom: null,
      option: null
    }
  },
  methods: {
    resize () {
      this.dom.resize()
    }
  },
  mounted () {
    const option = {
      tooltip: {
        trigger: 'axis',
        axisPointer: {
          type: 'shadow'
        }
      },
      legend: {
        data: ['垃圾车', '快递车', '清扫车', '巡逻车']
      },
      grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
      },
      xAxis: [
        {
          type: 'category',
          data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
        }
      ],
      yAxis: [
        {
          type: 'value'
        }
      ],
      series: [
        {
          name: '垃圾车',
          type: 'bar',
          stack: '在线车辆',
          data: [232, 247, 260, 256, 268, 270, 280]
        },
        {
          name: '快递车',
          type: 'bar',
          stack: '在线车辆',
          data: [44, 51, 56, 59, 67, 63, 67]
        },
        {
          name: '清扫车',
          type: 'bar',
          stack: '在线车辆',
          data: [79, 92, 116, 143, 192, 160, 156]
        },
        {
          name: '巡逻车',
          type: 'bar',
          stack: '在线车辆',
          data: [200, 200, 200, 200, 200, 200, 200]
        }
      ]
    }
    this.$nextTick(() => {
      this.dom = echarts.init(this.$refs.dom, 'tdTheme')
      this.dom.setOption(option, true)
    })
    on(window, 'resize', this.resize)
  },
  beforeDestroy () {
    off(window, 'resize', this.resize)
  }
}
</script>

<style scoped>

</style>
