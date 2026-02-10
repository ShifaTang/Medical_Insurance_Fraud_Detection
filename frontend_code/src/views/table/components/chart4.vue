<template>
  <ve-bar-chart :data="chartData" :settings="chartSettings" />
</template>

<script>
module.exports = {
  created () {
    this.chartData = {
      dimensions: {
        name: 'Repo',
/*
['基本统筹基金支付金额_SUM','本次审批金额_SUM','药品费申报金额_SUM','药品费发生金额_SUM',
                     '月药品金额_MAX','月统筹金额_AVG','治疗费申报金额_SUM','ALL_SUM']
['统筹支付金额_SUM','月就诊次数_MAX','就诊次数_SUM','起付标准以上自负比例金额_SUM',
                            '可用账户报销金额_SUM','非账户支付金额_SUM','医院_统筹金_AVG',
                            '月就诊天数_MAX','月就诊天数_AVG','月统筹金额_MAX'] 
                            
['医院_统筹金_MAX','贵重药品发生金额_SUM','医疗救助个人按比例负担金额_SUM',
                           '医疗救助医院申请_SUM','个人账户金额_SUM','一天去两家医院的天数']                     
*/

        data: [
          '基本统筹基金支付金额_SUM', '本次审批金额_SUM', '药品费申报金额_SUM RA', '药品费发生金额_SUM', '月药品金额_MAX',
          '月统筹金额_AVG', '治疗费申报金额_SUM', 'ALL_SUM',
          '统筹支付金额_SUM','月就诊次数_MAX','就诊次数_SUM','起付标准以上自负比例金额_SUM','可用账户报销金额_SUM','非账户支付金额_SUM','医院_统筹金_AVG','月就诊天数_MAX','月就诊天数_AVG','月统筹金额_MAX'
        ].reverse()
      },
      measures: [{
        name: '在11种特征提取方法中各特征出现次数',
        data: [11, 10, 10, 9, 9, 9, 8, 7, 7, 7,6,6,6,5,5,5,5,5].reverse()
      }]
    }
    this.chartSettings = {
      direction: 'row'
    }
  }
}
</script>
