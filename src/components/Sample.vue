<template>
  <div class="sample">
    <div ref="content">
      <h2>SAMPLE</h2>
    </div>
    <div ref="result">
    </div>
  </div>
</template>

<script>
import html2canvas from 'html2canvas'

export default {
  name: 'Sample',
  props: {},
  mounted: function() {
    html2canvas(this.$refs.content).then((canvas) => {
      this.$refs.result.appendChild(canvas)
    })
  },
}
</script>

<style scoped>

</style>
