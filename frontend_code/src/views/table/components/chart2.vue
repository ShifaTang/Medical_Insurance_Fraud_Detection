<template>
  <ve-treemap-chart :data="chartData" />
</template>

<script>
module.exports = {
  created () {
    this.chartData = {
      measures: [{
        name: '虚假贫困户信息',
        value: 172
      }, {
        name: '倒卖药品',
        value: 155
      }, {
        name: '滥用保险报销',
        value: 110
      }, {
        name: '联合欺诈',
        value: 103
      }, {
        name: '虚假诊疗项目欺诈',
        value: 64
      }, {
        name: '虚假就医',
        value: 61
      }, {
        name: '非法获取医疗补助',
        value: 44
      }, {
        name: '欺诈类型 8',
        value: 33
      }, {
        name: '欺诈类型 9',
        value: 22
      }]
    }
  }
}
</script>
