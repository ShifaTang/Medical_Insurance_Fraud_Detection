<template>
  <div>
    <el-upload
      class="upload-demo"
      action="https://jsonplaceholder.typicode.com/posts/"
      :on-success="handleSuccess"
      :file-list="fileList"
      multiple>
      <el-button size="small" type="primary">点击上传</el-button>
    </el-upload>

    <el-divider></el-divider>

    <el-table
      :data="uploadedFiles"
      border
      style="width: 100%">
      <el-table-column
        prop="name"
        label="文件名">
      </el-table-column>
      <el-table-column
        label="操作">
        <template slot-scope="scope">
          <el-button size="mini" type="primary" @click="downloadFile(scope.row)">下载</el-button>
          <el-button size="mini" type="success" @click="importFile(scope.row)">导入</el-button>
          <el-button size="mini" type="danger" @click="removeFile(scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>

    <el-divider></el-divider>

    <el-table
      :data="importedFiles"
      border
      style="width: 100%">
      <el-table-column
        prop="name"
        label="已导入的文件">
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      fileList: [],
      uploadedFiles: [],
      importedFiles: [],
      aass:[]
    };
  },
  methods: {
    async handleSuccess(response, file, fileList) {
      // 上传成功后将文件添加到 uploadedFiles 列表中
      this.uploadedFiles.push({ name: file.name, url: file.url });
      this.fileList.pop();


      try {
        // 发送文件信息到后端
        const response = await axios.post('http://127.0.0.1:8001/upload/uploadfile', { name: file.name, url: file.url });
        // 处理后端返回的响应数据
        console.log('文件上传成功，后端返回数据:', response.data);
      } catch (error) {
        // 处理请求失败的情况
        console.error('上传文件失败:', error);
      }





    },
    downloadFile(file) {
      // 下载文件的逻辑
      // 可以通过文件的url进行下载操作
      window.open(file.url, '_blank');
    },
    importFile(file) {
      // 导入文件的逻辑
      // 将成功导入的文件添加到 importedFiles 列表中
      this.importedFiles.push({ name: file.name });
    },
    removeFile(file) {
      // 删除文件的逻辑
      const index = this.uploadedFiles.findIndex(f => f.name === file.name);
      if (index !== -1) {
        this.uploadedFiles.splice(index, 1);
      }
    }
  }
}
</script>
