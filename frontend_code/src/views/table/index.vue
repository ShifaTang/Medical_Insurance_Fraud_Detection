<template>
  <div>
    <div>
      <el-row>
        <el-col :span="12"><div class="grid-content bg-purple">
          <div>
            <chart4 class="small-chart">特征因子排名</chart4>
            <h1 class="centered-text">特征因子排名</h1>
          </div>
        </div></el-col>
        <el-col :span="12"><div class="grid-content bg-purple-light">
          <div>
            <chart1 class="small-chart">异常比例</chart1>
            <h1 class="centered-text">异常比例</h1>
          </div>
        </div></el-col>
      </el-row>
    </div>
    <div>
      <el-row>
        <el-col :span="12"><div class="grid-content bg-purple">
          <div>
            <chart2 class="small-chart">欺诈类别</chart2>
            <h1 class="centered-text">欺诈类别</h1>
          </div>
        </div></el-col>
        <el-col :span="12"><div class="grid-content bg-purple-light">
          <div>
            <chart3 class="small-chart">月就诊人数</chart3>
            <h1 class="centered-text">月就诊人数</h1>
          </div>
        </div></el-col>
      </el-row>
    </div>





  </div>
</template>

<script>
import chart1 from "./components/chart1.vue"
import chart2 from "./components/chart2.vue"
import chart3 from "./components/chart3.vue"
import chart4 from "./components/chart4.vue"

export default {
  components: {
    chart1,
    chart2,
    chart3,
    chart4
  }
}
</script>

<style>
.small-chart {
  width: 100%;
  height: auto; /* 设置图表容器的高度为自适应高度 */
}

.centered-text {
  text-align: center;
}
</style>
