<script>
// see https://www.chartjs.org/docs/latest/charts/radar.html
import { Radar, mixins } from 'vue-chartjs'

export default {
  extends: Radar,
  mixins: [mixins.reactiveProp],
  props: ['chartData', 'options'],
  mounted () {
    this.renderChart(this.chartData, this.options)
  }
}
</script>
