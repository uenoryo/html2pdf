<script>
// see https://www.chartjs.org/docs/latest/charts/radar.html
import { Bar } from 'vue-chartjs'

export default {
  extends: Bar,
  props: ['data', 'option'],
  mounted () {
    this.renderChart(this.data, this.option)
  }
}
</script>
