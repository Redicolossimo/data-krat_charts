<script>
import {
  Bar,
  mixins
} from 'vue-chartjs'
export default {
  extends: Bar,
  mixins: [mixins.reactiveProp],
  data: () => ({

  }),
  props: {
    chartData: {
      type: Object,
      default: null
    },
    options: {
      type: Object,
      default: null
    },
    hideChart: {
      type: Number,
      default: null,
    }
  },
  mounted () {
    this.renderChart(this.chartData, this.options)
  },
  watch: {
    chartData () {
      this.renderChart(this.chartData, this.options)
    }
  },
}
</script>
