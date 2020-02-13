<template>
  <div class="sample">
    <div ref="content">
      <h2>SAMPLE</h2>
    </div>
    <div ref="result">
    </div>
    <hr>
    <div>
      <button @click="save">保存</button>
    </div>
  </div>
</template>

<script>
import html2canvas from 'html2canvas'
import jsPDF from 'jspdf'

export default {
  name: 'Sample',
  props: {},
  mounted: function() {
    html2canvas(this.$refs.content).then((canvas) => {
      this.$refs.result.appendChild(canvas)
    })
  },
  methods: {
    "save": function() {
      let pdf = new jsPDF()
      html2canvas(this.$refs.content).then((canvas) => {
        pdf.addImage(canvas.toDataURL(), 'JPEG', 0, 0, 200, 0)
        pdf.save('test.pdf')
      })
    },
  },
}
</script>

<style scoped>

</style>
