<template>
  <ve-bar-chart :data="chartData" :settings="chartSettings" />
</template>

<script>
module.exports = {
  created () {
    this.chartData = {
      dimensions: {
        name: 'Month',
        data: ['Jan.', 'Feb.', 'Mar.', 'Apr.', 'May.', 'Jun.', 'Jul']
      },
      measures: [{
        name: '异常',
        data: [9, 28, 30, 25, 46, 654, 1]
      }, {
        name: '正常',
        data: [103, 106, 152, 253, 674, 13917, 2]
      }]
    }
    this.chartSettings = {
      stack: {
        sum: ['异常' ,'正常']
      }
    }
  }
}
</script>
