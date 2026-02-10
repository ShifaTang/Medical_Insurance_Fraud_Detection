<template>
  <ve-pie-chart :data="chartData" />
</template>

<script>
module.exports = {
  created () {
    this.chartData = {
      dimensions: {
        name: '类别',
        data: ['异常', '正常']
      },
      measures: [{
        name: '人数',
        data: [793, 15207]
      }]
    }
  }
}
</script>
