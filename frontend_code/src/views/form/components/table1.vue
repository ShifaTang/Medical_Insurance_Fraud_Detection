<template>
  <div class="container">
    <div class="component-one">

      <!-- 查询ID的方法框 -->
      <div class="input">
        <el-input v-model="searchId" placeholder="请输入要查询的编号"></el-input>
      </div>


      <!-- 表格组件 -->
      <el-table
        ref="filterTable"
        :data="filteredData"
      >
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
        <el-table-column label="操作">
          <template slot-scope="scope">
            <el-button
              size="mini"
              @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
            <el-button
              size="mini"
              type="danger"
              @click="handleDelete(scope.$index, scope.row)">删除</el-button>
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
      <!-- 添加按钮 -->
      <el-button class="el-btn" type="primary" @click="showAddDialog">添加</el-button>
      <!-- 添加对话框 -->
      <el-dialog
        title="添加编号"
        :visible.sync="dialogVisible"
        width="30%">
        <el-input v-model="newId" placeholder="请输入编号"></el-input>
        <span slot="footer" class="dialog-footer">
          <el-button @click="dialogVisible = false">取消</el-button>
          <el-button type="primary" @click="handleConfirm">确认</el-button>
        </span>
      </el-dialog>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      tableData: [
        // {
        //   id: '202184823'
        // },
        // {
        //   id: '202184824'
        // }
        // 省略其他数据
      ],
      currentPage: 1,
      pageSize: 10,
      searchId: '', // 用户查询的ID
      selectedId: null ,// 选中的ID
      dialogVisible: false, // 对话框是否可见
      newId: '' // 新添加的编号
    }
  },created:function(){
    axios.get('http://47.100.173.31:8002/query/prohibit-list').then(res=>{
      this.tableData = res.data
      // console.log(res.data)
    })
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

    handleAdd() {
      this.dialogVisible = true;
    },
    handleEdit(index, row) {
      // 弹出对话框让用户输入新的编号
      this.$prompt('请输入新的编号', '编辑', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        inputPattern: /^\d+$/, // 编号格式为数字
        inputErrorMessage: '编号格式不正确'
      }).then(({ value }) => {
        // 用户点击确定后的回调
        // 在这里可以根据新的编号进行相应的操作
        console.log('用户输入的新编号为：', value);
        // 更新表格数据中的编号
        this.tableData[index].id = value;
        this.$message({
          type: 'success',
          message: '编辑成功!'
        });
      }).catch(() => {
        // 用户点击取消后的回调
        console.log('用户取消了编辑操作');
      });
    },
    handleDelete(index, row) {
      // 在这里实现删除功能，你可以弹出一个确认对话框，确认后删除该行数据
      this.$confirm('确定删除该行数据吗?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        // 确认删除
        this.tableData.splice(index, 1);
        this.$message({
          type: 'success',
          message: '删除成功!'
        });
      }).catch(() => {
        // 取消删除
        this.$message({
          type: 'info',
          message: '已取消删除'
        });
      });
    },
    showAddDialog() {
      this.dialogVisible = true;
    },
    handleConfirm() {
      // 检查表格数据中是否已存在相同的编号
      const existingItem = this.tableData.find(item => item.id === this.newId);
      if (existingItem) {
        // 如果表格数据中已存在相同的编号，不执行添加操作
        this.$message.error('编号已存在，请重新输入');
        return;
      }
      // 确认添加
      this.tableData.push({ id: this.newId });
      this.dialogVisible = false;
    }
  }
}
</script>

<style>
.component-one{
  display: flex;
  flex-direction: column!important;
}

.el-btn{
  margin-right: 10px;
  width: 100px;
}
</style>
