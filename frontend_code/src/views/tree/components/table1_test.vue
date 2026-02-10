<template xmlns="http://www.w3.org/1999/html">
  <div>
    <div v-if="loading">正在加载数据...</div>

    <div v-else>
  <div class="container" style="position: relative;">
    <div class="component-one">
      <!-- 查询ID的方法框 -->
      <div>
        <el-input v-model="searchId" placeholder="请输入要查询的编号"></el-input>
        <!-- 表格组件 -->
        <el-table
          ref="filterTable"
          :data="filteredData"
          style="width: 100%"
          @selection-change="handleSelectionChange"
          @row-click="handleRowClick"
        >
          <el-table-column
            type="selection"
            width="55">
          </el-table-column>

          <el-table-column
            label="序号"
            type="index"
            width="60">
          </el-table-column>

          <el-table-column
            prop="personal_id"
            label="编号"
            width="180">
          </el-table-column>

          <el-table-column
            prop="prob_res"
            label="标签"
            width="100"
            :filters="[{ text: '异常', value: true }, { text: '正常', value: false }]"
            :filter-method="filterTag"
            filter-placement="bottom-end">
            <template slot-scope="scope">
              <el-tag
                :type="scope.row.prob_res === true ? 'primary' : 'success'"
                disable-transitions>{{ scope.row.prob_res == true ? '异常' : '正常' }}</el-tag>
            </template>
          </el-table-column>
        </el-table>

        <!-- 分页组件 -->
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage"
          :page-sizes="[10, 20, 30, 40]"
          :page-size="pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="tableData.length">
        </el-pagination>
        <el-button @click="sendMessages" type="primary">发送提示信息</el-button>
      </div>
    </div>
  </div>

</div>


</div>

</template>

<script>
import { eventBus } from '../store/eventBus';
import table2 from "./table2_test.vue"
import table3 from "./table3_test.vue"
import axios from 'axios';
export default {
  components: {
    table2,
    table3
  },
  data() {
    return {
      loading:true,
      selectedRowData: null, // 存储选中行数据
      fraud_type1: ['基本统筹基金支付金额_SUM','本次审批金额_SUM','药品费申报金额_SUM','药品费发生金额_SUM'],
      fraud_type2: ['月药品金额_MAX','月统筹金额_AVG','治疗费申报金额_SUM','ALL_SUM'],
                     
      tableData: [
        // {
        //   personal_id: '202400001',
        //   prob_res: true,
        //   fraud_prob:0,
        //   fraud_types: '正常',
        //   pos: [40000, 27800, 22000, 20200, 15600, 13600,23000],
        //   feature1: ["特征1","特征2","特征3","特征4"],
        //   feature2: ["特征1","特征2","特征3","特征4"]
        // },
        // {
        //   personal_id: '202400001',
        //   prob_res: true,
        //   fraud_prob:0,
        //   fraud_types: '正常',
        //   pos: [40000, 2783450, 22450, 20200, 155300, 136540,230540],
        //   feature1: ["特征1","特征2","特征3","特征4"],
        //   feature2: ["特征1","特征2","特征3","特征4"]
        // }
      ],
      currentPage: 1,
      pageSize: 10,
      searchId: '', // 用户查询的ID
      selectedId: null // 选中的ID
    }
  },
  created:function(){
      axios.get("http://47.100.173.31:8002/query/person-fraud-info").then((res) =>{
        this.tableData = res.data
      })

          setTimeout(() => {
        // 完成数据请求，将loading设置为false
        this.loading = false;
        // 其他数据处理操作
      }, 2000);
          
      // })
    console.log(this.tableData)
    console.log(this.fraud_type1)

  },
  computed: {
    // 根据查询的ID过滤数据
    filteredData() {
      let filteredData = this.tableData;
      if (this.searchId) {
        filteredData = filteredData.filter(item => item.personal_id.includes(this.searchId));
      }
      const startIndex = (this.currentPage - 1) * this.pageSize;
      const endIndex = startIndex + this.pageSize;
      return filteredData.slice(startIndex, endIndex);
    }
  },
  methods: {
    filterTag(value, row) {

      return row.prob_res === value; // 返回异常数据

    },
    handleSizeChange(val) {
      this.pageSize = val;
    },
    handleCurrentChange(val) {
      this.currentPage = val;
    },
    // 选择发送信息
    handleSelectionChange(selection) {
      this.selectedRows = selection;
    },
    sendMessages() {
      // 模拟发送提示信息
      if (this.selectedRows.length > 0) {
        this.$message.success('发送信息成功');
      } else {
        this.$message.warning('请选择至少一行数据');
      }
    },
    handleRowClick(row) {
      // this.loading=false
      // 将选中行的数据赋值给 selectedRowData
      this.selectedRowData = row;
      // this.loading=true
      eventBus.$emit('rowDataSelected', row);
    }
  }
}
</script>
<style>
.container {
  display: flex;
}

.component-one {
  width: 1200px;
  flex-direction: row;
  display:flex ;
  margin-right: 20px; /* 给组件一右侧留出一些空间 */
}

.component-two {
  width:404px;
}
.component-three {
  width:404px;
}
</style>
