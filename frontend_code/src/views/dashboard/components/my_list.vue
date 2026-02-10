<!-- <template>
  <div class="table-container">
    <el-table :data="tableData" border stripe class="custom-table">
      <el-table-column prop="title" label="Title" min-width="100%">
        <template slot-scope="scope">
          <a :href="scope.row.link" target="_blank">{{ scope.row.title }}</a>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage"
      :page-sizes="[7, 14, 21, 28]"
      :page-size="pageSize"
      layout="total, sizes, prev, pager, next, jumper"
      :total="tableData.length"
      class="pagination">
    </el-pagination>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        { id: 1, title: '国家医疗保障局党组传达学习习近平总书记在二十届中央纪委三次全会上的重要讲话精神', link: 'http://www.nhsa.gov.cn/art/2024/1/15/art_14_11961.html' },
        { id: 2, title: '国家医疗保障局党组传达学习习近平总书记在二十届中央纪委三次全会上的重要讲话精神', link: 'https://example.com/2' },
        { id: 3, title: '国家医疗保障局党组传达学习习近平总书记在二十届中央纪委三次全会上的重要讲话精神', link: 'https://example.com/3' },
        { id: 4, title: '国家医疗保障局党组传达学习习近平总书记在二十届中央纪委三次全会上的重要讲话精神', link: 'http://www.nhsa.gov.cn/art/2024/1/15/art_14_11961.html' },
        { id: 5, title: '国家医疗保障局党组传达学习习近平总书记在二十届中央纪委三次全会上的重要讲话精神', link: 'https://example.com/2' },
        { id: 6, title: '国家医疗保障局党组传达学习习近平总书记在二十届中央纪委三次全会上的重要讲话精神', link: 'https://example.com/3' },
        { id: 7, title: '国家医疗保障局党组传达学习习近平总书记在二十届中央纪委三次全会上的重要讲话精神', link: 'http://www.nhsa.gov.cn/art/2024/1/15/art_14_11961.html' },
        // Add more data as needed
      ],
      currentPage: 1,
      pageSize: 10
    };
  },
  methods: {
    handleSizeChange(val) {
      this.pageSize = val;
    },
    handleCurrentChange(val) {
      this.currentPage = val;
    }
  }
};
</script>

<style scoped>
.table-container {
  width: 100%; /* 设置表格容器的宽度 */

}

.custom-table {
  width: 100%; /* 设置表格宽度为100%，充满容器 */

}

.pagination {
  margin-top: 20px; /* 设置分页组件与表格的间距 */

}
</style> -->

<template>
  <div class="table-container">
    <el-table :data="displayedData" border stripe class="custom-table">
      <el-table-column prop="title" label="Title" min-width="100%">
        <template slot-scope="scope">
          <a :href="scope.row.link" target="_blank">{{ scope.row.title }}</a>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage"
      :page-sizes="[5, 10, 21, 28]"
      :page-size="pageSize"
      layout="total, sizes, prev, pager, next, jumper"
      :total="totalItems"
      class="pagination">
    </el-pagination>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        { id: 1, title: '国家医疗保障局党组传达学习习近平总书记在二十届中央纪委三次全会上的重要讲话精神', link: 'http://www.nhsa.gov.cn/art/2024/1/15/art_14_11961.html' },
        { id: 2, title: '国家医疗保障局召开党组会议 贯彻落实习近平总书记重要指示精神-全力帮助甘肃临夏州积石山县做好抗震救灾工作', link: 'https://example.com/2' },
        { id: 3, title: '国家医保局组织开展“一人一档”参保信息管理研讨工作', link: 'https://example.com/3' },
        { id: 4, title: '全国医疗保障工作会议在京召开', link: 'http://www.nhsa.gov.cn/art/2024/1/15/art_14_11961.html' },
        { id: 5, title: '江西撑开“医保大伞”为群众幸福“加码”', link: 'https://example.com/2' },
        { id: 6, title: '关于执行《江西省医保药品分类与代码数据库(2023年)》的通知', link: 'https://example.com/3' },
        { id: 7, title: '2024年湖南省医疗保障工作会议在长沙召开', link: 'http://www.nhsa.gov.cn/art/2024/1/15/art_14_11961.html' },
        { id: 8, title: '国家医疗保障局党组传达学习习近平总书记在二十届中央纪委三次全会上的重要讲话精神', link: 'http://www.nhsa.gov.cn/art/2024/1/15/art_14_11961.html' },
        { id: 9, title: '国家医疗保障局召开党组会议 贯彻落实习近平总书记重要指示精神-全力帮助甘肃临夏州积石山县做好抗震救灾工作', link: 'https://example.com/2' },
        { id: 10, title: '国家医保局组织开展“一人一档”参保信息管理研讨工作', link: 'https://example.com/3' },
        { id: 11, title: '全国医疗保障工作会议在京召开', link: 'http://www.nhsa.gov.cn/art/2024/1/15/art_14_11961.html' },
        { id: 12, title: '江西撑开“医保大伞”为群众幸福“加码”', link: 'https://example.com/2' },
        { id: 13, title: '关于执行《江西省医保药品分类与代码数据库(2023年)》的通知', link: 'https://example.com/3' },
        { id: 14, title: '2024年湖南省医疗保障工作会议在长沙召开', link: 'http://www.nhsa.gov.cn/art/2024/1/15/art_14_11961.html' },
        // Add more data as needed
      ],
      currentPage: 1,
      pageSize: 5
    };
  },
  computed: {
    // 根据 currentPage 和 pageSize 计算当前页面需要展示的数据
    displayedData() {
      const startIndex = (this.currentPage - 1) * this.pageSize;
      const endIndex = startIndex + this.pageSize;
      return this.tableData.slice(startIndex, endIndex);
    },
    // 根据 currentPage 和 pageSize 计算总条数
    totalItems() {
      return this.tableData.length;
    }
  },
  methods: {
    handleCurrentChange(val) {
      this.currentPage = val;
    },
    handleSizeChange(val) {
      this.pageSize = val;
    }
  }
};
</script>

<style scoped>
.table-container {
  width: 100%; /* 设置表格容器的宽度 */
}

.custom-table {
  width: 100%; /* 设置表格宽度为100%，充满容器 */
}

.pagination {
  margin-top: 20px; /* 设置分页组件与表格的间距 */
}
</style>


