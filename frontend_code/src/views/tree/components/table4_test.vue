<template>
  <div>
    <div>
      <el-table
        :data="tableData1"
        border
        style="width: 100%">
        <el-table-column
          prop="one"
          label="特征因子1"
          width="135">
          <template slot-scope="scope">
            <span style="color: #222; font-weight: bold;">{{ scope.row.one }}</span>
          </template>
        </el-table-column>
        <el-table-column
          prop="two"
          label="特征因子2"
          width="135">
          <template slot-scope="scope">
            <span style="color: #222; font-weight: bold;">{{ scope.row.one }}</span>
          </template>
        </el-table-column>
        <el-table-column
          prop="three"
          label="特征因子3"
          width="135">
          <template slot-scope="scope">
            <span style="color: #222; font-weight: bold;">{{ scope.row.one }}</span>
          </template>
        </el-table-column>
        <el-table-column
          prop="four"
          label="特征因子4"
          width="135">
          <template slot-scope="scope">
            <span style="color: #222; font-weight: bold;">{{ scope.row.one }}</span>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <div>
      <el-table
        :data="tableData2"
        border
        style="width: 100%">
        <el-table-column
          prop="one"
          label="特征因子1"
          width="135">
          <template slot-scope="scope">
            <span style="color: #222; font-weight: bold;">{{ scope.row.one }}</span>
          </template>
        </el-table-column>
        <el-table-column
          prop="two"
          label="特征因子2"
          width="135">
          <template slot-scope="scope">
            <span style="color: #222; font-weight: bold;">{{ scope.row.one }}</span>
          </template>
        </el-table-column>
        <el-table-column
          prop="three"
          label="特征因子3"
          width="135">
          <template slot-scope="scope">
            <span style="color: #222; font-weight: bold;">{{ scope.row.one }}</span>
          </template>
        </el-table-column>
        <el-table-column
          prop="four"
          label="特征因子4"
          width="135">
          <template slot-scope="scope">
            <span style="color: #222; font-weight: bold;">{{ scope.row.one }}</span>
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>


</template>

<script>
import { eventBus } from '../store/eventBus';
export default {
  data() {
    return {
      tableData1: [],
      tableData2: []
    }
  },
  created() {
    // 监听事件，接收数据
    eventBus.$on('rowDataSelected', (row) => {
      // 从接收到的数据中提取特征因子信息，根据你的数据结构自行修改
      this.tableData1 = [{
        one: row.feature1[0],
        two: row.feature1[1],
        three: row.feature1[2],
        four: row.feature1[3]
      }];

      this.tableData2 = [{
        one: row.feature2[0],
        two: row.feature2[1],
        three: row.feature2[2],
        four: row.feature2[3]
      }];
    });
  }
}
</script>
