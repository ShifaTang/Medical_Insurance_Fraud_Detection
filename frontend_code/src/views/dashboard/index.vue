<template>
<!--  <div class="dashboard-container">-->
<!--    <div class="dashboard-text">name: {{ name }}</div>-->
<!--  </div>-->
  <div>
    <div>
      <!--    轮播图-->
      <lunbo></lunbo>
    </div>
    <div>
      <!--新闻列表-->
<list></list>
    </div>
    <div>
      <test1></test1>
    </div>
  </div>

</template>

<script>
import { mapGetters } from 'vuex'
import lunbo from "./components/carousel.vue"
import list from "./components/my_list.vue"
import test from "./components/test.vue"
import test1 from "./components/test1.vue"
export default {
  name: 'Dashboard',
  computed: {
    ...mapGetters([
      'name'
    ])
  },
  components: {
    lunbo,
    list,
    test,
    test1
  }
}
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
</style>
