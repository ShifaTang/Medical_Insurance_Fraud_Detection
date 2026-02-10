<!-- <template>
  <div :class="className" :style="{height:height,width:width}" />
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
import resize from '../mixins/resize'

export default {
  mixins: [resize],
  props: {
    rowData: {
      type: Object,
      default: null
    },
    className: {
      type: String,
      default: 'chart'
    },
    width: {
      type: String,
      default: '404px'
    },
    height: {
      type: String,
      default: '300px'
    }
  },
  data() {
    return {
      chart: null
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.initChart();
      this.setupData();//后面加的
    });
  },
  beforeDestroy() {
    // if (!this.chart) {
    //   return
    // }
    // this.chart.dispose()
    // this.chart = null
    //下面后面加的
    if (this.chart) {
      this.chart.dispose();
      this.chart = null;
    }

  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$el, 'macarons')
      var propValue=this.rowData.pos[0].value
      var propValue2=this.rowData.pos[1].value
      var propValue3=this.rowData.pos[2].value
      var propValue4=this.rowData.pos[3].value
      var propValue5=this.rowData.pos[4].value
      this.chart.setOption({
        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b} : {c} ({d}%)'
        },
        legend: {
          left: 'center',
          bottom: '10',
          data: ['Industries', 'Technology', 'Forex', 'Gold', 'Forecasts']
        },
        series: [
          {
            name: 'WEEKLY WRITE ARTICLES',
            type: 'pie',
            roseType: 'radius',
            radius: [15, 95],
            center: ['50%', '38%'],
            data: [
              { value: propValue, name: 'Industries' },
              { value: propValue2, name: 'Technology' },
              { value:propValue3, name: 'Forex' },
              { value: propValue4, name: 'Gold' },
              { value: propValue5, name: 'Forecasts' }
            ],
            animationEasing: 'cubicInOut',
            animationDuration: 2600
          }
        ]
      })
    }
  }
}
</script>

 -->

 <template>
  <div :class="className" :style="{height: height, width: width}" ref="chartContainer" />
</template>

<script>
import echarts from 'echarts';

export default {
  props: {
    rowData: {
      type: Object,
      default: null
    },
    className: {
      type: String,
      default: 'chart'
    },
    width: {
      type: String,
      default: '404px'
    },
    height: {
      type: String,
      default: '300px'
    }
  },
  data() {
    return {
      chart: null
    };
  },
  mounted() {
    this.initChart();

    // 监视rowData的变化
    this.$watch('rowData', () => {
      this.setupData();
    }, { deep: true });
  },
  beforeDestroy() {
    if (this.chart) {
      this.chart.dispose();
      this.chart = null;
    }
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$refs.chartContainer, 'macarons');
      this.setupData(); // 初始化时设置初始数据
    },
    setupData() {
      if (!this.chart || !this.rowData) {
        return;
      }
      // 根据this.rowData设置echarts图表数据和配置
      // ...
    }
  }
};
</script>





