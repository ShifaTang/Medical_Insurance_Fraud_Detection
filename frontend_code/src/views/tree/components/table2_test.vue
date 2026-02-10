<template>
  <el-row>
    <el-col :span="9">
      <div class="grid-content bg-purple">
        <el-card :body-style="{ padding: '0px' ,maxHeight: '90px'}">
          <el-card style="display: flex; align-items: center;">
            <img src="../img/sva1.svg" class="image" style="margin-right: 8px;">
            <h2 style="font-size: 17px">欺诈概率:{{rowData.fraud_prob}}</h2>
          </el-card>
        </el-card>
      </div>

    </el-col>
    <el-col :span="15">
      <div class="grid-content bg-purple">
        <el-card :body-style="{ padding: '0px' ,maxHeight: '90px'}">
          <el-card style="display: flex; align-items: center;">
            <img src="../img/sva2.svg" class="image" style="margin-right: 8px;">
            <h2 style="font-size: 17px">欺诈种类:{{rowData.fraud_types}}</h2>
          </el-card>
        </el-card>
      </div>
    </el-col>
  </el-row>
</template>


<style>
.image {
  width: 10%;
  display: block;
}
</style>

<script>
import { eventBus } from '../store/eventBus';
export default {
  data() {
    return {
      // currentDate: new Date()
      rowData: null // 存储接收到的数据
    };
  },
  created() {
    // 监听事件，接收数据
    eventBus.$on('rowDataSelected', (row) => {
      this.rowData = row;
    });
  }
}
</script>
