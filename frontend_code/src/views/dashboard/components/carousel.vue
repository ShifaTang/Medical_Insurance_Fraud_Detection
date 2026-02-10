<template>
  <el-carousel :interval="4000" type="card" height="200px">
    <el-carousel-item v-for="image in images" :key="image.id">
      <img :src="image.src" :alt="image.alt"  class="carousel-image">
    </el-carousel-item>
  </el-carousel>
</template>

<script>
export default {
  data() {
    return {
      images: [
        { id: 1, src: require('../../../assets/lunbo/2024年湖南省医疗保障工作会议在长沙召开.png'), alt: 'Image 1' },
        { id: 2, src:require( '../../../assets/lunbo/全国医疗保障工作会议在京召开.png'), alt: 'Image 2' },
        { id: 3, src: require('../../../assets/lunbo/湖南召开国家谈判药品落地保障政策研讨会.png'), alt: 'Image 3' },
        // Add more image data as needed
      ]
    };
  }
}
</script>
<style scoped>
.carousel-image {
  width: 100%; /* 设置图片宽度为100% */
  height: 100%; /* 根据宽度自适应高度，保持图片比例不变 */
  object-fit: cover;
}

</style>
