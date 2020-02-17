<script>
// see https://www.chartjs.org/docs/latest/charts/radar.html
import { Radar } from 'vue-chartjs'

export default {
  extends: Radar,
  props: ['chartdata', 'options'],
  mounted () {
    this.renderChart(this.chartdata, this.options)
  }
}
</script>
