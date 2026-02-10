<template xmlns="http://www.w3.org/1999/html">
  <div class="container">
    <div class="component-one">
      <!-- 查询ID的方法框 -->
      <div>
        <el-input v-model="searchId" placeholder="请输入要查询的编号"></el-input>

        <!-- 表格组件 -->
        <el-table
          ref="filterTable"
          :data="filteredData"
          style="width: 100%"
          @row-click="handleRowClick"
          @selection-change="handleSelectionChange"
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
            prop="id"
            label="编号"
            width="180">
          </el-table-column>
          <el-table-column
            prop="tag"
            label="标签"
            width="100"
            :filters="[{ text: '异常', value: '异常' }, { text: '正常', value: '正常' }]"
            :filter-method="filterTag"
            filter-placement="bottom-end">
            <template slot-scope="scope">
              <el-tag
                :type="scope.row.tag === '异常' ? 'primary' : 'success'"
                disable-transitions>{{scope.row.tag}}</el-tag>
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

      <!-- 传递选中的ID给组件二 -->
      <div>
        <table2 class='component-two' :selectedId="selectedId" v-if="selectedId" @selected-id-changed="handleSelectedIdChanged" ></table2>
        <table3 :rowData="selectedRowData"></table3>
      </div>

    </div>

  </div>
</template>

<script>
import table2 from "./table2.vue"
import table3 from "@/views/tree/components/table3.vue";
export default {
  components: {
    table3,
    table2
  },
  data() {
    return {
      tableData: [
        {
          id: '202184823',
          tag: '异常'
        },
        {
          id: '202184824',
          tag: '正常'
        },
        {
          id: '202184823',
          tag: '异常'
        },
        {
          id: '202184824',
          tag: '正常'
        },
        {
          id: '202184823',
          tag: '异常'
        },
        {
          id: '202184824',
          tag: '正常'
        },
        {
          id: '202184823',
          tag: '异常'
        },
        {
          id: '202184824',
          tag: '正常'
        },
      ],
      currentPage: 1,
      pageSize: 10,
      searchId: '', // 用户查询的ID
      selectedId: null // 选中的ID
    }
  },
  computed: {
    // 根据查询的ID过滤数据
    filteredData() {
      let filteredData = this.tableData;
      if (this.searchId) {
        filteredData = filteredData.filter(item => item.id.includes(this.searchId));
      }
      const startIndex = (this.currentPage - 1) * this.pageSize;
      const endIndex = startIndex + this.pageSize;
      return filteredData.slice(startIndex, endIndex);
    }
  },
  methods: {
    filterTag(value, row) {
      return row.tag === value;
    },
    handleSizeChange(val) {
      this.pageSize = val;
    },
    handleCurrentChange(val) {
      this.currentPage = val;
    },
    handleRowClick(row) {
      this.selectedId = row.id; // 将选中行的ID保存到selectedId中
      this.$emit('selected-id-changed', this.selectedId); // 发送选中的ID给父组件
    },
    handleSelectionChange(selection) {
      this.selectedRows = selection;
    },
    sendMessages() {
      // 模拟发送提示信息
      // 实际情况中，你可以在这里发送请求向后端发送信息
      // 这里只是一个简单的示例
      if (this.selectedRows.length > 0) {
        this.$message.success('发送信息成功');
      } else {
        this.$message.warning('请选择至少一行数据');
      }
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
