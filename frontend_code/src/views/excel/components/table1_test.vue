<template>
  <el-table :data="tableData" stripe style="width: 100%">
    <el-table-column prop="date" label="文件名" width="180" />
    <el-table-column prop="name" label="上传者" width="180" />
    <el-table-column prop="address" label="上传时间" width="180" />
    <el-table-column fixed="right" label="操作" />
    <template #default>
      <el-button link type="primary" size="small" @click="handleClick()"
      >导入</el-button
      >
      <el-button link type="primary" size="small">下载</el-button>
    </template>
  </el-table>
</template>

<script>

export default {
  data(){
    return{
      tableData:[
        {
          date: '2016-05-03',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
        },
        {
          date: '2016-05-02',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
        },
        {
          date: '2016-05-04',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
        },
        {
          date: '2016-05-01',
          name: 'Tom',
          address: 'No. 189, Grove St, Los Angeles',
        },
      ]
    }
  },
  handleClick(){
    console.log('click')
  }
}
</script>
