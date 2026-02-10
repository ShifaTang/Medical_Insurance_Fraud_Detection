<template>
  <ve-pie-chart :data="chartData" :settings="chartSettings" />
 </template>

 <script>
 
 import { eventBus } from '../store/eventBus';

 export default{
  data() {
   return {
    //临时加的
    // temp: null,
    chartData: null, // 存储接收到的数据
    chartSettings: null // 存储接收到的设置
   };
  },
  created () {
    // axios.get('http://47.100.173.31:8002/query/prohibit-list').then(res=>{
    //   this.tableData = res.data
    //   // console.log(res.data)
    // })


   eventBus.$on('rowDataSelected', (row) => {
    this.chartData = {
      //这是加的
      // this:loading = true,
   dimensions: {
     name: '金额分布',
    data: ['药品费申报金额', '贵重药品发生金额', '中成药费发生金额','中草药费发生金额', 
     '检查费申报金额', '贵重检查费金额', '治疗费申报金额','医用材料发生金额']
    },
    measures: [{
     name: '金额',
   data: row.pos
  // data: [40560, 27800, 22000, 20270, 15600, 13680,23070]
   }]
 
    };
    this.chartSettings = {   roseType: 'radius',
   radius: [30, 110],
   center: ['50%', '65%'], // 将圆心下移
    };
   });

   console.log(this.chartData)
   console.log("hahahah")
   console.log(this.chartSettings)
   
   //这是加的
  //  this.loading = false; // 假设数据加载完成后移除 loading 状态

  }
 }
 
 </script>


 <!-- <template>
  <ve-pie-chart :data="chartData" :settings="chartSettings" />
</template>

<script>
  module.exports = {
    created () {
      this.chartData = {
        dimensions: {
          name: '渠道',
          data: ['APP', 'PC', 'M端', '微信', '手Q', '小程序']
        },
        measures: [{
          name: 'PV',
          data: [403400, 278430, 22040, 2022300, 15230, 13600]
        }]
      }
      this.chartSettings = {
        roseType: 'radius',
        radius: [30, 110]
      }
    }
  }
</script> -->
